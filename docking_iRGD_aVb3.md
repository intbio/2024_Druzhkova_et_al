
## Visualisation of docking solutions for the iRGD-integrin aV/b3 complex 
[Back](https://intbio.org/2024_TRAIL_MD/)

<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
<br>
  <p style="color:#d6d6d6;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">Integrin aV (PDB ID 1L5G, chain A)</p>
  <br />
  <p style="color:#FFF2CC;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">Integrin b3 (PDB ID 1L5G, chain B)</p>

<table border="solid 1px;" style="font-size:14px;">
<tr>
<th> Show </th> <th>Model </th> <th> GalazyDock score </th><th>Energy, kkal/mol </th><th>Download PDB </th>
</tr>

<tbody>
  
  <script src="https://unpkg.com/ngl@2.0.0-dev.35/dist/ngl.js"></script>
  <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
  <script>
  

   var names = ['docking_str/iRGD_aVb3_1.pdb', 'docking_str/iRGD_aVb3_2.pdb', 'docking_str/iRGD_aVb3_3.pdb', 'docking_str/iRGD_aVb3_4.pdb', 'docking_strS/iRGD_aVb3_5.pdb', 'docking_str/iRGD_aVb3_6.pdb', 'docking_str/iRGD_aVb3_7.pdb', 'docking_str/iRGD_aVb3_8.pdb', 'docking_str/iRGD_aVb3_9.pdb', 'docking_str/iRGD_aVb3_10.pdb']
   var models = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   var galaxy_scores = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   var energies = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
   peptide_reps = [];
    $(document).ready(function() {
      window.stage = new NGL.Stage("viewport",{ backgroundColor:"#FFFFFF" });
      window.stage.loadFile("docking_str/aVb3.pdb").then(function (ref_pdb) {
        var aspectRatio = 2;
        var radius = 1.5;

        ref_pdb.addRepresentation('cartoon', {
           "sele": ":A", "color": 0xd6d6d6,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });;
	ref_pdb.addRepresentation('cartoon', {
           "sele": ":B", "color": '#FFF2CC',"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });;
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
                   "sele": ":C", "color": hyper_scheme});
                repr.setVisibility(false);
                peptide_reps.push(repr);
               
          	});
		}
    
    window.stage.viewerControls.spin( [ 0, 1, 0 ],110 )
    });
    var i
    for (i= 0; i < arrayLength; i++) {
        
        document.write(`<tr><td> <input type="checkbox" id="${i}" name="${names[i]}"></td> <td>  ${models[i]}  </td> <td> ${galaxy_scores[i]} </td><td> ${energies[i]} </td><td> <a href="https://intbio.org/2024_TRAIL_MD/${names[i]}" download>PDB</a> </td></tr>`); 
			}
		  
      
$('input[type=checkbox]').on('change', toggle_reference_structure);

function toggle_reference_structure() {
               var state = $(this).is(":checked");
               var nameid = $(this).attr('id');
               peptide_reps[nameid].setVisibility(state)
          }

  </script>
  <div id="viewport" style="width:500px; height:500px; border: thin solid black"></div>
  </tbody>	
</table>
</body>
</html>
