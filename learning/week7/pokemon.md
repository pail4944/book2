# Pokemon

Create interactive visualizations for the Pokemon data. Complete the script
so that when a user clicks on each menu button, there will be a different
bar chart shown in the Viz block.

You will be reusing the code you wrote for generating SVG bar charts a couple weeks
ago. The main challenge is to figure out how to connect your visualization code
with the front-end code (event handlers ... etc).

## Menu

<button id="viz-horizontal">Attack (Horizontal Bars)</button>
<button id="viz-vertical">Attack (Vertical Bars)</button>
<button id="viz-attack-defense">Attack vs. Defense</button>
<button id="viz-speed-defense">Speed vs. Defense</button>
<button id="viz-horizontal-sorted">Attack (sorted from low to high)</button>
<button id="viz-horizontal-sorted-desc">Attack (sorted from high to low)</button>
<button id="viz-attack-speed">Attack (width) vs. Speed (color)</button>

## Viz

<div class="myviz" style="width:100%; height:500px; border: 1px black solid;">
Data is not loaded yet
</div>

{% script %}
// pokemonData is a global variable
pokemonData = 'not loaded yet'

$.get('http://pail4944.github.io/book2/data/pokemon-small.json')
 .success(function(data){
     console.log('data loaded', data)
     $('.myviz').html('number of records load:' + data.length)
	 pokemonData = data
 })


function vizAsHorizontalBars(){

 var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
					<text transform="translate(0 15)"> \
						${d.label} \
					</text> \
                    </g>'

    var template = _.template(tplString)
	
    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }
	
	function computeLabel(d, i){
		return d.Name
	}
    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
					label: computeLabel(d, i)
				}
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}
function vizAsVerticalBars(){

    var tplString = '<g transform="translate(${d.x} ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="${d.height}"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
                    </g>'

    
    var template = _.template(tplString)

    function computeX(d, i) {
        return i*20
    }

    function computeWidth(d, i) {
        return 20
    }
	function computeHeight(d, i){
		return d.Attack
	}
    function computeY(d, i) {
        return 0
    }

    function computeColor(d, i) {
        return 'red'
    }

    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    height: computeHeight(d, i),
					width: computeWidth(d, i),
                    color: computeColor(d, i)
                }
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}
function vizAsAttackDefenseBars(){

    var tplString = '<g transform="translate(120 ${d.y})"> \
                    <rect x="-${d.attack}" width="${d.attack}" height="20" style="fill:red; stroke-width:1; stroke:rgb(0,0,0)" /> \
					<rect x=0 width="${d.defense}" height="20" style="fill:blue; stroke-width:1; stroke:rgb(0,0,0)" /> \
					<text transform="translate(0 15)"> ${d.label} </text> \
                    </g>'

    var template = _.template(tplString)

    function computeX(d, i) {
		return 120
	}

	function computeA(d, i) {
		return d.Attack
	}

	function computeD(d, i) {
		return d.Defense
	}

	function computeY(d, i) {
		return i * 20
	}

	function computeColor(d, i) {
		return 'red'
	}

	function computeLabel(d, i) {
		return d.Name
	}
	var viz = _.map(pokemonData, function(d, i){
            return {
                x: computeX(d, i),
                y: computeY(d, i),
                attack: computeA(d,i),
				defense: computeD(d,i),
                color: computeColor(d, i),
				label: computeLabel(d, i)
            }
         })
	console.log(viz)

	var result = _.map(viz, function(d){
         // invoke the compiled template function on each viz data
         return template({d: d})
     })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}

function vizAsSpeedDefenseBars(){

    var tplString = '<g transform="translate(120 ${d.y})"> \
                    <rect x="-${d.speed}" width="${d.speed}" height="20" style="fill:red; stroke-width:1; stroke:rgb(0,0,0)" /> \
					<rect x=0 width="${d.defense}" height="20" style="fill:blue; stroke-width:1; stroke:rgb(0,0,0)" /> \
					<text transform="translate(0 15)"> ${d.label} </text> \
                    </g>'

    var template = _.template(tplString)

    function computeX(d, i) {
		return 120
	}

	function computeS(d, i) {
		return d.Speed
	}

	function computeD(d, i) {
		return d.Defense
	}

	function computeY(d, i) {
		return i * 20
	}

	function computeColor(d, i) {
		return 'red'
	}

	function computeLabel(d, i) {
		return d.Name
	}
	var viz = _.map(pokemonData, function(d, i){
            return {
                x: computeX(d, i),
                y: computeY(d, i),
                speed: computeS(d,i),
				defense: computeD(d,i),
                color: computeColor(d, i),
				label: computeLabel(d, i)
            }
         })
	console.log(viz)

	var result = _.map(viz, function(d){
         // invoke the compiled template function on each viz data
         return template({d: d})
     })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}
function vizAsHorizontalSortedBars(){

    var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
					<text transform="translate(0 15)"> \
						${d.label} \
					</text> \
                    </g>'

    var template = _.template(tplString)
	pokemonDataasc = _.sortBy(pokemonData, function(d){
		return d.Attack
	})
    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }
	function computeLabel(d, i){
		return d.Name
	}
    var viz = _.map(pokemonDataasc, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
					label: computeLabel(d, i)
				}
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}
function vizAsHorizontalSortedDescBars(){

     var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
					<text transform="translate(0 15)"> \
						${d.label} \
					</text> \
                    </g>'

    var template = _.template(tplString)
	pokemonDatadesc = _.sortBy(pokemonData, function(d){
		return d.Attack
	}).reverse()
    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
        return 'red'
    }
	function computeLabel(d, i){
		return d.Name
	}
    var viz = _.map(pokemonDatadesc, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
					label: computeLabel(d, i)
				}
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}


function vizAsAttackSpeedBars(){


     var tplString = '<g transform="translate(0 ${d.y})"> \
                    <rect   \
                         width="${d.width}" \
                         height="20"    \
                         style="fill:${d.color};    \
                                stroke-width:3; \
                                stroke:rgb(0,0,0)" />   \
					<text transform="translate(0 15)"> \
						${d.label} \
					</text> \
                    </g>'

    var template = _.template(tplString)
	
    function computeX(d, i) {
        return 0
    }

    function computeWidth(d, i) {        
        return d.Attack
    }

    function computeY(d, i) {
        return i * 20
    }

    function computeColor(d, i) {
		var maxspeed = _.max(_.pluck(pokemonData, 'Speed'))
		var color = (d.Speed  / maxspeed) * 255
		color = Math.round(color)
		return 'rgb(' + color + ',0,0)'
	}
	
	function computeLabel(d, i){
		return d.Name
	}
    var viz = _.map(pokemonData, function(d, i){
                return {
                    x: computeX(d, i),
                    y: computeY(d, i),
                    width: computeWidth(d, i),
                    color: computeColor(d, i),
					label: computeLabel(d, i)
				}
             })
    console.log('viz', viz)

    var result = _.map(viz, function(d){
             // invoke the compiled template function on each viz data
             return template({d: d})
         })
    console.log('result', result)

    $('.myviz').html('<svg>' + result + '</svg>')
}


$('button#viz-horizontal').click(vizAsHorizontalBars)
$('button#viz-vertical').click(vizAsVerticalBars)
$('button#viz-attack-defense').click(vizAsAttackDefenseBars)
$('button#viz-speed-defense').click(vizAsSpeedDefenseBars)
$('button#viz-horizontal-sorted').click(vizAsHorizontalSortedBars)
$('button#viz-horizontal-sorted-desc').click(vizAsHorizontalSortedDescBars)
$('button#viz-attack-speed').click(vizAsAttackSpeedBars)


{% endscript %}
