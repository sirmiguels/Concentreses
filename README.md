Concentreses
============
<!DOCTYPE HTML PUBLIC>
<html>
<head>
<title>Concentrese</title>
<meta http-equiv="Content-Type" content="text/html; charset=iso-8859-1">
<script language="JavaScript">

var directorio = "imagenes" 
var numImagenes = 32 
perder = 30
var nums=new Array()
var cant = 16
var acrtos = 0
var intentos = 0
gana = false
perdio = false
function numero(){
var num = Math.ceil(Math.random() *numImagenes);
return num}

nums[0] = numero()

for(m=1;m<=(cant-1);m++)
{
nums[m] =  comprueba(numero())
}

function comprueba(nume)
{
var repe = false
for(t=0;t<nums.length;t++)
	{
	if(nume == nums[t])
		{
		repe = true; break
		}
	}
if(repe == false)
	{
	return nume
	}
else
	{
	m--
	comprueba(numero())
	}
}
var lista = new Array()
largo = nums.length
for(w = 0; w < largo ; w++)
	{
	nums[largo + w] = nums[w]
	}

var numero = 0
function comprueba2(number)
{
if(nums[number] == null)
	{
	if(number == nums.length-1)
		{
		number = 0
		number2 = number
		comprueba2(number2)
		}
	else
		{
		number += 1
		number2 = number
		comprueba2(number2)
		}
	}
else{
numero = number
return number
	}
}

for(q=0; q < nums.length; q++)
	{
	if(q == nums.length-1)
		{
		for(e=0;e < nums.length; e++)
			{
			if(nums[e] != null)
				{
				lista[q] = nums[e];
				break
				}
			}
		}
		else
			{
			numerin = Math.floor(Math.random() * nums.length-1)
			numerin = comprueba2(numerin)
			lista[q] = nums[numero]
			nums[numero] = null
			}
	}
	
var imagenes = new Array()

for(n=0;n<lista.length;n++)
	{
	imagenes[n] = new Image()
	imagen = eval('"' + lista[n] + '.jpg"')
	imagenes[n].src = directorio + "/" + imagen
	}


s = 1

document.writeln ('<table align="center">')
document.writeln ('<tr align="center">')
for(p=1; p<=nums.length;p++)
	{
	if(s > 4){document.write ('</tr><tr>');s=1}
	document.write ('<td id="' + lista[p-1] + '"><a href="#" onclick="this.blur();return false">')
	document.write ('<img id="' + lista[p-1] + '" onclick="gira(this,this.id)" src="' + directorio + '/fondo.gif" width="64" height="64">')
	document.writeln ('</a></td>')
	s++
	}
document.writeln ('</table>')
cont = 0 
var gi1,gi2
function gira(cual,carta)
{
if(perdio == true)
	{
	document.formu.visor.value="Termino Juego"
	setTimeout('document.location.reload()',2000)
	}
if(cual != gi1){cont++}
if(cont < 3)
	{
	cual.src = directorio + "/" + carta + ".jpg"
	if(cont==1){gi1 = cual;}
	else{gi2 = cual; comp()}
	}
	
}
function comp()
{
if(gi1.src == gi2.src)
	{
	setTimeout("gi1.style.borderColor='blue'",200)
	setTimeout("gi2.style.borderColor='blue'",400)
	gi1.onclick=null;gi2.onclick=null
	intentos++
	document.formu.visor.value = "Intentos: " + intentos
	acrtos++
	if(acrtos == cant) 
		{
		finJuego('gana')
		gana = true
		}
	
	cont = 0
	}
else 
	{
	setTimeout("restaura()",1500)
	
	}

}
function restaura()
	{
	gi1.src = directorio + "/" + "fondo.gif" ; gi1 =""
	setTimeout('gi2.src = directorio + "/fondo.gif";gi2=""',200)
	cont = 0
	intentos ++
	document.formu.visor.value = "Intentos: " + intentos
	if(intentos >= perder)
		{
		cont = 4
		finJuego('pierde')
		perdio = true
		}
	}
function finJuego(cual)
{
if(navigator.appName == "Netscape")
	{
	anchoVentana = window.innerWidth
	altoVentana = window.innerHeight
	}
else
	{
	anchoVentana = document.body.scrollWidth
	altoVentana = document.body.scrollHeight
	}
document.getElementById('gana').style.top=(altoVentana -100)/2
document.getElementById('gana').style.left =(anchoVentana -200)/2
if(cual == 'pierde'){document.getElementById('mensaje').innerHTML = 'intentos ' + perder + ' intentos<br> Perdiste  :-(';cont='perdio'}
document.getElementById('gana').style.visibility = 'visible'
}
function cierra()
{document.getElementById('gana').style.visibility='hidden'}
</script>
<style type="text/css">
<!--
.formato {
	font-family: Tahoma, Verdana, Arial;
	font-size: 12px;
	font-weight: bold;
	border: 1px solid #990000;
}

-->
</style>
</head>

<body bgcolor="#FFFFFA" onload="document.formu.visor.value = 'Intentos: 0';">

<div align="center">
  <form name="formu" style="border:0">
    <input name="visor" type="text" class="formato" size="13" value="Intentos: 0" >
  </form>
  <a href="javascript:location.reload()"><strong><font size="2">Nuevo Juego</font></strong></a> 
</div>
</body>
</html>
