
## Visualisation of docking solutions for the iRGD-NRP1 complex 
[Back](https://intbio.org/2024_Druzhkova_et_al/)

<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
<br>
  <p style="color:#d6d6d6;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">NRP1, a2-b1-b2 domains (PDB ID 2QQM)</p>
 
<table border="solid 1px;" style="font-size:14px;">
<tr>
<th> Show </th> <th>Model </th> <th> GalazyDock score </th><th>Energy, kcal/mol (FoldX) </th><th>Energy, kcal/mol (MMPBSA) </th><th>Download PDB </th>
</tr>

<tbody>
  
  <script src="https://unpkg.com/ngl@2.0.0-dev.35/dist/ngl.js"></script>
  <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
  <script>
  

   var names = ['docking_str/iRGD_NRP1_1.pdb', 'docking_str/iRGD_NRP1_2.pdb', 'docking_str/iRGD_NRP1_3.pdb', 'docking_str/iRGD_NRP1_4.pdb', 'docking_str/iRGD_NRP1_5.pdb', 'docking_str/iRGD_NRP1_6.pdb', 'docking_str/iRGD_NRP1_7.pdb', 'docking_str/iRGD_NRP1_8.pdb', 'docking_str/iRGD_NRP1_9.pdb', 'docking_str/iRGD_NRP1_10.pdb']
   var models = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   var galaxy_scores = [0.612,0.612,0.612,0.612,0.612,0.612,0.612,0.612,0.612,0.612]
   var energies = [-3.044,-3.461,-0.735,-4.107,-2.758,-4.899,-3.311,-0.054,-2.199,-6.453]
   var mmpbsa = ['-26.16 ± 1.01','-20.97 ± 1.25','NA','-20.02 ± 0.93','-35.54 ± 0.12','-24.27 ± 0.25','-38.66 ± 0.48','NA','NA','-24.22 ± 1.73']
   peptide_reps = [];
    $(document).ready(function() {
      window.stage = new NGL.Stage("viewport",{ backgroundColor:"#FFFFFF" });
      window.stage.loadFile("docking_str/iRGD_NRP1_1.pdb").then(function (ref_pdb) {
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
        ["cyan", "*"]
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
        
        document.write(`<tr><td> <input type="checkbox" id="${i}" name="${names[i]}"></td> <td>  ${models[i]}  </td> <td> ${galaxy_scores[i]} </td><td> ${energies[i]} </td></td><td> ${mmpbsa[i]} </td><td> <a href="https://intbio.org/2024_Druzhkova_et_al/${names[i]}" download>PDB</a> </td></tr>`); 
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
