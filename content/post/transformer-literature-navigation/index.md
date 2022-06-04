---
title: Literature graph navigation with tranformers
date: 2020-09-20
math: true
diagram: true
highlight: true
image:
  placement: 3
  caption: ''
---

(check out my personal blog [here](https://mylonasc.github.io/2020-09-20-scholarclustering/) for other projects)

{{< toc >}} 

# Literature Clustering for Workshop
I co-organized some small workshops in my department (Civil and Environmental Engineering) called "[DSML@DBAUG](https://chatzi.ibk.ethz.ch/smm-news/2020/10/dsml.html)" where researchers (Ph.D. and Post Docs) from all chairs of the civil and geomatic engineering at ETH shortly presented their work. Since this was happening during the pandemic, everything happened through zoom. In order to be able to interact during the event, "breakout" sessions were scheduled where loosely moderated discussions around pre-defined topics were conducted among small groups. 

When considering how to split the participants, this presented with an interesting challenge: We would have liked to split the participants according to their interests.
At the same time, we couldn't easily find common current research interests among the participants since we are not familiar with all the participants. 
One of my interests is NLP applications, so naturally, I thought about finger-printing the authors according to their published abstracts, or at least have some graph of publications of the participants and their relevance so people can have a better idea who may have some interesting research that they'd like to meed.
Classical NLP topic modeling approaches first popped to mind, like performing some simple tf-idf featurization and then non-negative matrix factorization or [latent Dirichlet allocation](https://scikit-learn.org/stable/modules/generated/sklearn.decomposition.LatentDirichletAllocation.html).
It turns out, the last couple of years, NLP made leaps for the problem of
representation learning, with the so-called *transformers*. 


# The Rise of the Transformers
Since the leap in performance in natural language translation achieved in [Attention is All You Need](https://papers.nips.cc/paper/7181-attention-is-all-you-need) and the 
demonstration of exceptional transfer learning performance with [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/abs/1810.04805) 
transformers are the main focus of modern NLP. If you are familiar with deep learning and you would like a crash course on what a transformer is, there are great sources to find out what this is all about. There are several other important developments worth mentioning, but it is my impression that these two papers were the most impactful by far.

Another highly impactful piece of work is huggingface 🤗. Huggingface is a repository for distributing pre-trained transformer architectures with some standardized interfaces. 
It is even possible to test some architectures before downloading them. I used the `BERT-base` multilingual cased model for all the experiments. The abstracts and titles are concatenated (to form a representation for the "paper"), tokenized, and passed through the transformer. The transformer is "headless" in the sense that it simply returns a vector. The 
output vector is of size $$ N_{tokens} \times N_{embedding} $$. 
Since I want an embedding that represents the whole sentence, I simply summed along with tokens for each paper representation and had vectors of size $$ N_{embedding} $$ to work with. 

## Data collection and Web Scraping
A list of the participants was used, and abstracts for conference and journal publications they have authored were scraped from google scholar.
Google Scholar had a relatively strict limit on maximum queries. This can be circumvented by scripting some VPN hoping [which I did later](https://github.com/mylonasc/vpn-swarm-scraper) just as a proof of concept and in case I ever need it in the future. The idea I started implementing is that I can also distribute the queries and have a query server and have some fault tolerance as well (for instance, what happens when a query fails etc.). 


### Dimensionality Reduction and Literature Clustering
As a next step, I computed a [Principal Component Analysis](https://en.wikipedia.org/wiki/Principal_component_analysis) of the derived vectors to yield a lower-dimensional representation of the embedding vectors. This is useful for computational reasons but also may yield better performance in terms of the accuracy of the results in this case. Namely, it is easier/faster to compute inner products to compute distances needed downstream, and it is possible that PCA indeed captures the main factors of variations of the vectors, revealing clusters of topics. This led me to a small excursion on [fast approximate inner product search](https://engineering.fb.com/2017/03/29/data-infrastructure/faiss-a-library-for-efficient-similarity-search/) techniques as I was thinking on how to perform the neighborhood search interactively, but I'll leave these ideas for another day, and on the end result I will simply have a literature graph with pre-computed distances.

Simple [spectral clustering](https://scikit-learn.org/stable/modules/clustering.html#spectral-clustering) was used in order to identify automatically potential clusters of topics in the literature. I am not entirely sure if spectral clustering worked well, but it seems that the distances computed using the PCA components allow for the construction of a relevance graph that makes sense on several occasions. As a measure of "similarity," I pair-wise inner products of the vectors or pair-wise Euclidean distances. Some scaling tricks were applied, and the neighbors of the constructed were manually inspected to check for interesting similarities.

When I was satisfied with the results, a GUI using `d3.js` was created (adapting [this template](http://bl.ocks.org/paulovn/9686202)).
Some results from these graphs are shown in the following:
![mapping related cluster](/litgraph/mapping.png)
![social related cluster](/litgraph/social_political_papers.png)

Note that there are some results from web-scraping that were not correct, but this did not seem to degrade the results a lot. On the contrary, some sociological references, for instance, seem to be more connected, validating that BERT does capture some semantic similarities between the respective abstracts.
Here is a [live version](https://galerkin.hopto.org/authors_visualization/) of the GUI.


<!---<iframe src="https://galerkin.hopto.org/authors_visualization/" width="800" height="640" allowfullscreen="allowfullscreen"></iframe>
 -->

<div id="movieNetwork"></div>
  <div id="sidepanel-viz">

    <div id="title-viz">
      <div>DSML@DBAUG Publications Network</div>

      <!-- <a href="javascript:void(0);" 
              onClick="zoomCall(0.5);" style="pointer-events: all;">+</a>
      <a href="javascript:void(0);" 
         onClick="zoomCall(-0.5);" style="pointer-events: all;">-</a> -->

      <img id="helpIcon" 
           src="help-question-48.png" title="Click for help" 
           onClick="toggleDiv('help');"/> 

    </div>    

    <div id="help" class="panel_off">
      <img src="close.png" style="float: right;" 
           onClick="toggleDiv('help');"/>
        <ul>
        <li>Hover over a node to see the publication title, and to highlight
        the publications related to it.</li>

        <li>Click on a node to show publication details. It will open up a
        side panel.</li>

        <li>On the publication details panel, you can click on the <em>target</em> 
        icon to center the graph on that movie. And clicking on the link to
        a related publication will move to that publication (in the graph and in the
        panel)</li>

        <li>You can use you usual browser controls to zoom and pan
        over the graph. If you zoom in when centred on a movie, the
        graph will expand around it.</li>

        <li>Above a certain zoom level, publication titles are automatically
        displayed for all the nodes.</li>
      </ul>
      For additional information, check the <strong><a href="" onClick="return toggleDiv('faq');">FAQ</a></strong>.
    </div>

    <div id="movieInfo" class="panel_off"></div>
  </div>

  <div id="faq" class="panel_off">
    <div id="close_faq">
      <img src="close.png" onClick="toggleDiv('faq');"/>
    </div>
    <dl>

      <dt>Where does this come from?</dt>

      <dd>The author names of the participants of the 1st DSML@DBAUG workshop 
      were extracted, and google scholar was scraped to  retrieve the most relevant 
      results when their names were searched. 

      Some of the participants did not have a google scholar account and 
      there was a limit on the maximum number of possible requests on google-scholar.
      Nevertheless, 670+ publications were scraped. Also, no care was taken to filter out wrong hits on  
      the author names (too much work). 

      When you hover over a node the author name and the neighbors are highlighted. 


      <dt>And how was this concrete "author network" made?</dt>
      <dd>This is how I did it:
        <ol style="margin: 0px;">
          <li> Google scholar web scraping (using a Selenium-based library called scholarly) was performed for the author names</li>
            <li> The first 20 results were kept (the results contain extended citation info - such as title, abstract, other authors, publication venue & year etc) </li>
            <li> The title and abstract were contatenated and a phrase embedding using a pre-trained transformer neural network were computed.</li>
            <li> A similarity between all the embeddings of the publications was then computed. This similarity is the edge weight between two nodes. </li>
        </ol>
      </dd>

      The visualization of the graph was adapted from <a href http://bl.ocks.org/paulovn/9686202/>this example</a>



    <dt>Credits</dt>
    <dd><em>
      Web scraper <a href="https://pypi.org/project/scholarly/">Scholarly python library</a><br/>
      Pre-trained transformer <a href="https://huggingface.co/transformers/model_doc/bert.html">BERT</a><br/>
    </em></dd>
  </div>


<script>
function D3ok() {

  // Some constants
  var WIDTH = 960 ,
      HEIGHT = 600 ,
      SHOW_THRESHOLD = 2.5;

  // Variables keeping graph state
  var activePublication= undefined;
  var currentOffset = { x : 0, y : 0 };
  var currentZoom = 1.;

  // The D3.js scales
  var xScale = d3.scale.linear()
    .domain([0, WIDTH])
    .range([0, WIDTH]);
  var yScale = d3.scale.linear()
    .domain([0, HEIGHT])
    .range([0, HEIGHT]);
  var zoomScale = d3.scale.linear()
    .domain([0.1,6])
    .range([0.1,6])
    .clamp(false);

/* .......................................................................... */

  // The D3.js force-directed layout
  var force = d3.layout.force()
    .charge(-50)
    .size( [WIDTH, HEIGHT] )
    .linkStrength( function(d,idx) { return d.weight; } );

  // Add to the page the SVG element that will contain the movie network
  var svg = d3.select("#movieNetwork").append("svg:svg")
    .attr('xmlns','https://www.w3.org/2000/svg')
    .attr("width", WIDTH)
    .attr("height", HEIGHT)
    .attr("id","graph")
    .attr("viewBox", "0 0 " + WIDTH + " " + HEIGHT )
    .attr("preserveAspectRatio", "xMidYMid meet");

  // Movie panel: the div into which the movie details info will be written
  movieInfoDiv = d3.select("#movieInfo");

  /* ....................................................................... */

  // Get the current size & offset of the browser's viewport window
  function getViewportSize( w ) {
    var w = w || window;
    if( w.innerWidth != null ) 
      return { w: w.innerWidth, 
	       h: w.innerHeight,
	       x : w.pageXOffset,
	       y : w.pageYOffset };
    var d = w.document;
    if( document.compatMode == "CSS1Compat" )
      return { w: d.documentElement.clientWidth,
	       h: d.documentElement.clientHeight,
	       x: d.documentElement.scrollLeft,
	       y: d.documentElement.scrollTop };
    else
      return { w: d.body.clientWidth, 
	       h: d.body.clientHeight,
	       x: d.body.scrollLeft,
	       y: d.body.scrollTop};
  }



  function getQStringParameterByName(name) {
    var match = RegExp('[?&]' + name + '=([^&]*)').exec(window.location.search);
    return match && decodeURIComponent(match[1].replace(/\+/g, ' '));
  }


  /* Change status of a panel from visible to hidden or viceversa
     id: identifier of the div to change
     status: 'on' or 'off'. If not specified, the panel will toggle status
  */
  toggleDiv = function( id, status ) {
    d = d3.select('div#'+id);
    if( status === undefined )
      status = d.attr('class') == 'panel_on' ? 'off' : 'on';
    d.attr( 'class', 'panel_' + status );
    return false;
  }


  /* Clear all help boxes and select a movie in the network and in the 
     movie details panel
  */
  clearAndSelect = function (id) {
    toggleDiv('faq','off'); 
    toggleDiv('help','off'); 
    selectPublication(id,true);	// we use here the selectPublication() closure
  }


  /* Compose the content for the panel with movie details.
     Parameters: the node data, and the array containing all nodes
  */
  function getPubInfo( n, nodeArray ) {
    info = '';
    info += '<div class=t style="float: right margin-top: 50px">' + n.title + ' </div>';
    info +=
    '<img src="close.png" class="action" style="top: 0px;" title="close panel" onClick="toggleDiv(\'movieInfo\');"/>' +
    '<img src="target-32.png" class="action" style="top: 280px;" title="center graph on movie" onclick="selectPublication('+n.index+',true);"/>';
    info+='<div class=f>'+n.abstract+'</div>';

    info += '<br/></div><div style="clear: both;">'
    
    info += '<div class=f><span class=l>Cluster</span>: <span class=g>' 
           + n.cluster + '</span></div>';
    if( n.author )
      info += '<div class=f><span class=l>Author</span>: <span class=d>' 
           + n.author+ '</span></div>';
    if( n.url )
      info += '<div class=f><span class=l>Url</span>: <span class=c>' 
           + n.url + '</span></div>';
    if( n.year )
      info += '<div class=f><span class=l>Year</span>: ' + n.year + "</div>"
           
          
    if( n.links ) {
      info += '<div class=f><span class=l>Related to</span>: ';
      n.links.forEach( function(idx) {
	info += '[<a href="javascript:void(0);" onclick="selectPublication('  
	     + idx + ',true);">' + nodeArray[idx].label + '</a>]' + '<div>'+nodeArray[idx].title+'</div></br>'
      });
      info += '</div>';
    }
    return info;
  }


  // *************************************************************************

  d3.json(
    //'movie-network-25-7-3.json',
    'authors_visualization/authors_with_affinities.json',
    function(data) {

    // Declare the variables pointing to the node & link arrays
    var nodeArray = data.nodes;
    var linkArray = data.links;

    minLinkWeight = 
      Math.min.apply( null, linkArray.map( function(n) {return n.weight;} ) );
    maxLinkWeight = 
      Math.max.apply( null, linkArray.map( function(n) {return n.weight;} ) );

    // Add the node & link arrays to the layout, and start it
    force
      .nodes(nodeArray)
      .links(linkArray)
      .start();


    // A couple of scales for node radius & edge width
    var node_size = d3.scale.linear()
      .domain([5,10])	// we know score is in this domain
      .range([1,16])
      .clamp(true);
    var edge_width = d3.scale.pow().exponent(8)
      .domain( [minLinkWeight,maxLinkWeight] )
      .range([1,3])
      .clamp(true);


    /* Add drag & zoom behaviours */
    svg.call( d3.behavior.drag()
	      .on("drag",dragmove) );

    svg.call( d3.behavior.zoom()
	      .x(xScale)
	      .y(yScale)
	      .scaleExtent([1, 6])
	      .on("zoom", doZoom) );

    // ------- Create the elements of the layout (links and nodes) ------

    var networkGraph = svg.append('svg:g').attr('class','grpParent');

    // links: simple lines
    var graphLinks = networkGraph.append('svg:g').attr('class','grp gLinks')
      .selectAll("line")
      .data(linkArray, function(d) {return d.source.id+'-'+d.target.id;} )
      .enter().append("line")
      .style('stroke-width', function(d) { return edge_width(d.weight);} )
      .attr("class", "link");

    // nodes: an SVG circle
    var col_array = ['#fff568', '#ffc400', '#ff9800', '#ff6e40', '#f4511e', '#ff5252', '#e53935', '#e57373', '#f48fb1', '#9575cd', '#ba68c8', '#8c9eff', '#90caf9', '#64b5f6', '#d4e157', '#afb42b', '#9ccc65', '#bcaaa4', '#a1887f', '#a67c52', '#cfd8dc', '#90a4ae', '#78909c'];
    var col_array = ['#fff568', '#f4511e', '#ff5252', '#e57373', '#9575cd', '#ba68c8', '#8c9eff', '#90caf9', '#64b5f6', '#d4e157', '#afb42b', '#9ccc65', '#bcaaa4', '#a1887f', '#a67c52', '#cfd8dc', '#90a4ae', '#78909c'];

    var graphNodes = networkGraph.append('svg:g').attr('class','grp gNodes')
      .selectAll("circle")
      .data( nodeArray, function(d){ return d.id; } )
      .enter().append("svg:circle")
      .attr('id', function(d) { return "c" + d.index; } )
      .attr('r', function(d) { return node_size(7 || 3); } )
      .attr('pointer-events', 'all')
      .on("click", function(d) { highlightGraphNode(d,true,this); } )    
      .on("click", function(d) { showMoviePanel(d); } )
      .on("mouseover", function(d) { highlightGraphNode(d,true,this);  } )
      .on("mouseout",  function(d) { highlightGraphNode(d,false,this); } )
      .attr('class', function(d) { return 'node clustercolor'+d.cluster;} );
    console.log(graphNodes)

    // labels: a group with two SVG text: a title and a shadow (as background)
    var graphLabels = networkGraph.append('svg:g').attr('class','grp gLabel')
      .selectAll("g.label")
      .data( nodeArray, function(d){return d.label} )
      .enter().append("svg:g")
      .attr('id', function(d) { return "l" + d.index; } )
      .attr('class','label');
   
    shadows = graphLabels.append('svg:text')
      .attr('x','-2em')
      .attr('y','-.3em')
      .attr('pointer-events', 'none') // they go to the circle beneath
      .attr('id', function(d) { return "lb" + d.index; } )
      .attr('class','nshadow')
      .text( function(d) { return d.label; } );

    labels = graphLabels.append('svg:text')
      .attr('x','-2em')
      .attr('y','-.3em')
      .attr('pointer-events', 'none') // they go to the circle beneath
      .attr('id', function(d) { return "lf" + d.index; } )
      .attr('class','nlabel')
      .text( function(d) { return d.label; } );


    /* --------------------------------------------------------------------- */
    /* Select/unselect a node in the network graph.
       Parameters are: 
       - node: data for the node to be changed,  
       - on: true/false to show/hide the node
    */
    function highlightGraphNode( node, on )
    {
      //if( d3.event.shiftKey ) on = false; // for debugging

      // If we are to activate a movie, and there's already one active,
      // first switch that one off
      if( on && activePublication!== undefined ) {
	highlightGraphNode( nodeArray[activePublication], false );
      }

      // locate the SVG nodes: circle & label group
      circle = d3.select( '#c' + node.index );
      label  = d3.select( '#l' + node.index );

      // activate/deactivate the node itself
      circle
	.classed( 'main', on );
      label
	.classed( 'on', on || currentZoom >= SHOW_THRESHOLD );
      label.selectAll('text')
	.classed( 'main', on );

      // activate all siblings
      Object(node.links).forEach( function(id) {
	d3.select("#c"+id).classed( 'sibling', on );
	label = d3.select('#l'+id);
	label.classed( 'on', on || currentZoom >= SHOW_THRESHOLD );
	label.selectAll('text.nlabel')
	  .classed( 'sibling', on );
      } );

      // set the value for the current active movie
      activePublication= on ? node.index : undefined;
    }


    /* --------------------------------------------------------------------- */
    /* Show the details panel for a publication AND highlight its node in 
       the graph. Also called from outside the d3.json context.
       Parameters:
       - new_idx: index of the movie to show
       - doMoveTo: boolean to indicate if the graph should be centered
         on the publication
    */
    selectPublication = function( new_idx, doMoveTo ) {

      console.log(new_idx);

      // do we want to center the graph on the node?
      doMoveTo = doMoveTo || false;
      if( doMoveTo ) {
	s = getViewportSize();
	width  = s.w<WIDTH ? s.w : WIDTH;
	height = s.h<HEIGHT ? s.h : HEIGHT;
	offset = { x : s.x + width/2  - nodeArray[new_idx].x*currentZoom,
		   y : s.y + height/2 - nodeArray[new_idx].y*currentZoom };
	repositionGraph( offset, undefined, 'move' );
      }
      // Now highlight the graph node and show its movie panel
      highlightGraphNode( nodeArray[new_idx], true );
      showMoviePanel( nodeArray[new_idx] );
    }


    /* --------------------------------------------------------------------- */
    /* Show the movie details panel for a given node
     */
    function showMoviePanel( node ) {
      // Fill it and display the panel
      movieInfoDiv
	.html( getPubInfo(node,nodeArray) )
	.attr("class","panel_on");
    }

	    
    /* --------------------------------------------------------------------- */
    /* Move all graph elements to its new positions. Triggered:
       - on node repositioning (as result of a force-directed iteration)
       - on translations (user is panning)
       - on zoom changes (user is zooming)
       - on explicit node highlight (user clicks in a movie panel link)
       Set also the values keeping track of current offset & zoom values
    */
    function repositionGraph( off, z, mode ) {

      // do we want to do a transition?
      var doTr = (mode == 'move');

      // drag: translate to new offset
      if( off !== undefined &&
	  (off.x != currentOffset.x || off.y != currentOffset.y ) ) {
	g = d3.select('g.grpParent')
	if( doTr )
	  g = g.transition().duration(500);
	g.attr("transform", function(d) { return "translate("+
					  off.x+","+off.y+")" } );
	currentOffset.x = off.x;
	currentOffset.y = off.y;
      }

      // zoom: get new value of zoom
      if( z === undefined ) {
	if( mode != 'tick' )
	  return;	// no zoom, no tick, we don't need to go further
	z = currentZoom;
      }
      else
	currentZoom = z;

      // move edges
      e = doTr ? graphLinks.transition().duration(500) : graphLinks;
      e
	.attr("x1", function(d) { return z*(d.source.x); })
        .attr("y1", function(d) { return z*(d.source.y); })
        .attr("x2", function(d) { return z*(d.target.x); })
        .attr("y2", function(d) { return z*(d.target.y); });

      // move nodes
      n = doTr ? graphNodes.transition().duration(500) : graphNodes;
      n
	.attr("transform", function(d) { return "translate("
					 +z*d.x+","+z*d.y+")" } );
      // move labels
      l = doTr ? graphLabels.transition().duration(500) : graphLabels;
      l
	.attr("transform", function(d) { return "translate("
					 +z*d.x+","+z*d.y+")" } );
    }
           

    /* --------------------------------------------------------------------- */
    /* Perform drag
     */
    function dragmove(d) {
      offset = { x : currentOffset.x + d3.event.dx,
		 y : currentOffset.y + d3.event.dy };
      repositionGraph( offset, undefined, 'drag' );
    }


    /* --------------------------------------------------------------------- */
    /* Perform zoom. We do "semantic zoom", not geometric zoom
     * (i.e. nodes do not change size, but get spread out or stretched
     * together as zoom changes)
     */
    function doZoom( increment ) {
      newZoom = increment === undefined ? d3.event.scale 
					: zoomScale(currentZoom+increment);
      if( currentZoom == newZoom )
	return;	// no zoom change

      // See if we cross the 'show' threshold in either direction
      if( currentZoom<SHOW_THRESHOLD && newZoom>=SHOW_THRESHOLD )
	svg.selectAll("g.label").classed('on',true);
      else if( currentZoom>=SHOW_THRESHOLD && newZoom<SHOW_THRESHOLD )
	svg.selectAll("g.label").classed('on',false);

      // See what is the current graph window size
      s = getViewportSize();
      width  = s.w<WIDTH  ? s.w : WIDTH;
      height = s.h<HEIGHT ? s.h : HEIGHT;

      // Compute the new offset, so that the graph center does not move
      zoomRatio = newZoom/currentZoom;
      newOffset = { x : currentOffset.x*zoomRatio + width/2*(1-zoomRatio),
		    y : currentOffset.y*zoomRatio + height/2*(1-zoomRatio) };

      // Reposition the graph
      repositionGraph( newOffset, newZoom, "zoom" );
    }

    zoomCall = doZoom;	// unused, so far

    /* --------------------------------------------------------------------- */

    /* process events from the force-directed graph */
    force.on("tick", function() {
      repositionGraph(undefined,undefined,'tick');
    });

    /* A small hack to start the graph with a movie pre-selected */
    mid = getQStringParameterByName('id')
    if( mid != null )
      clearAndSelect( mid );
  });

} // end of D3ok()
</script>

<script>
          var head = document.getElementsByTagName('head')[0];
          var script = document.createElement('script');
          script.type = 'text/javascript';
	  script.src = "https://d3js.org/d3.v3.min.js";
          script.addEventListener('load', D3ok, false);
          script.onload = "D3ok();";
	  head.appendChild(script);
</script>


<div>HERE!</div>
<iframe src="authors_visualization/index.html" width="800" height="640" allowfullscreen="allowfullscreen"></iframe>

## Final thoughts
We ended up not using this for splitting the participants of the workshops; it was a fun project which I may continue in the future. I used a library called [scholarly](https://pypi.org/project/scholarly/) which had some limitations. If you would go about doing that yourself I would recommend [Selenium](https://selenium-python.readthedocs.io/). 

I hope you enjoyed reading about this project, as much as I enjoyed making it! 

<h3></h3><!-- Start BawkBox Code--><script data-sil-id="603555d83c0d090013685d06">var loadWidget = function() { var d = document, w = window, l = window.location,p = l.protocol == "file:" ? "http://" : "//"; if (!w.WS) w.WS = {}; c = w.WS; var m=function(t, o){ var e = d.getElementsByTagName("script"); e=e[e.length-1]; var n = d.createElement(t); if (t=="script") {n.async=true;} for (k in o) n[k] = o[k]; e.parentNode.insertBefore(n, e)}; m("script", { src: p + "bawkbox.com/widget/like-dislike/603555d83c0d090013685d06?page=" +encodeURIComponent(l+''), type: 'text/javascript' }); c.load_net = m; }; if(window.Squarespace){ document.addEventListener('DOMContentLoaded', loadWidget); setTimeOut(function(){ document.addEventListener('DOMContentLoaded', loadWidget); }, 3000) } else { loadWidget() } </script><div class="sil-widget-like-dislike sil-widget" id="sil-widget-603555d83c0d090013685d06"><a href="//bawkbox.com/install/like-dislike">Like Dislike Button</a></div><!-- End BawkBox Code-->
