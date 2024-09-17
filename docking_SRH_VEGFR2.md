
## Visualisation of docking solutions for the SRH-VEGFR2 complex 
[Назад](https://intbio.org/2024_TRAIL_MD/)

<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
<br>
  <p style="color:#d6d6d6;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">VEGFR2, d2-d3 domains (PDB ID 2X1W)</p>
<!--   <p style="color:#fc03ec;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black">Пептид EARGIHCHSIR</p> -->
 
<table border="solid 1px;" style="font-size:14px;">
<tr>
<th> Show </th><th> GalazyDock score </th><th>Energy, kkal/mol </th>
</tr>

<tbody>
  
  <script src="https://unpkg.com/ngl@2.0.0-dev.35/dist/ngl.js"></script>
  <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
  <script>
  

   var names = ['docking_str/SRH_VEGFR2_1.pdb', 'docking_str/SRH_VEGFR2_2.pdb', 'docking_str/SRH_VEGFR2_3.pdb', 'docking_str/SRH_VEGFR2_4.pdb', 'docking_strS/RH_VEGFR2_5.pdb', 'docking_str/SRH_VEGFR2_6.pdb', 'docking_str/SRH_VEGFR2_7.pdb', 'docking_str/SRH_VEGFR2_8.pdb', 'docking_str/SRH_VEGFR2_9.pdb', 'docking_str/SRH_VEGFR2_10.pdb']
   var models = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   var galaxy_scores = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   var energies = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   peptide_reps = [];
    $(document).ready(function() {
      window.stage = new NGL.Stage("viewport",{ backgroundColor:"#FFFFFF" });
      window.stage.loadFile("VEGFR2.pdb").then(function (ref_pdb) {
        var aspectRatio = 2;
        var radius = 1.5;

        ref_pdb.addRepresentation('cartoon', {
           "sele": ":A ", "color": 0xd6d6d6,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });;
        ref_pdb.autoView();
      });

      var arrayLength = names.length;
      var k;

    var hyper_scheme = NGL.ColormakerRegistry.addSelectionScheme([
        ["orange", ".CA"],
        ['0xecf0f1', '_H'],
        ["blue", "_N"],
        ["red", "_O"],
        ["magenta", "*"]
      ], "DA");
		for (k = 0; k < arrayLength; k++) {
            window.stage.loadFile(`${names[k]}`).then(function (ref_pdb) {
                var repr = ref_pdb.addRepresentation('hyperball', {
                   "sele": ":B", "color": hyper_scheme});
                repr.setVisibility(false);
                peptide_reps.push(repr);
               
          	});
		}
    
    window.stage.viewerControls.spin( [ 0, 1, 0 ],110 )
    });
    var arrayLength = names.length;
			for (var i = 0; i < arrayLength; i++) {
        
        document.write(`<tr><td> <input type="checkbox" id="${i}" name="${models[i]}"></td><td> ${galaxy_score[i]} </td><td> ${energies[i]} </td></tr>`); 
			}
      
$('input[type=checkbox]').on('change', toggle_reference_structure);

function toggle_reference_structure() {
               var state = $(this).is(":checked");
               var name = $(this).attr('id');
               peptide_reps[name].setVisibility(state)
          }


  </script>
  <div id="viewport" style="width:500px; height:500px; border: thin solid black"></div>
  </tbody>	
</table>
</body>
</html>
