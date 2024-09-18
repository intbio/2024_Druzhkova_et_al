## Визуализация *ab-initio* докинга полипептидов на нуклеосому, содержащую гистоновый вариант H2A.1
[Назад](https://intbio.org/grant_2018_RNFmoluch/year3.html)

<html lang="en">
<head>
  <meta charset="utf-8">
</head>
<body>
<br>
  <p style="color:#94b4d1;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">H3</p> 
  <p style="color:#94d19c;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">H4</p>
  <p style="color:#d6d989;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">H2A</p>
  <p style="color:#d98989;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">H2B</p>
  <p style="color:#d6d6d6;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black;display: inline">ДНК</p>
<!--   <p style="color:#fc03ec;font-size:22px;font-family:verdana;font-weight: bold;text-shadow: -1px 0 black, 0 1px black, 1px 0 black, 0 -1px black">Пептид EARGIHCHSIR</p> -->
 
<table border="solid 1px;" style="font-size:14px;">
<tr>
<th> Show </th><th>Sequence </th> <th>Energy, kkal/mol </th>
</tr>

<tbody>
  
  <script src="https://unpkg.com/ngl@2.0.0-dev.35/dist/ngl.js"></script>
  <script src="https://code.jquery.com/jquery-3.5.1.min.js" integrity="sha256-9/aliU8dGd2tb6OSsuzixeV4y/faTqgFtohetphbbj0=" crossorigin="anonymous"></script>
  <script>
  

   var names = ['docking_str/SRH_VEGFR2_1.pdb', 'docking_str/SRH_VEGFR2_2.pdb', 'docking_str/SRH_VEGFR2_3.pdb', 'docking_str/SRH_VEGFR2_4.pdb', 'docking_strS/RH_VEGFR2_5.pdb', 'docking_str/SRH_VEGFR2_6.pdb', 'docking_str/SRH_VEGFR2_7.pdb', 'docking_str/SRH_VEGFR2_8.pdb', 'docking_str/SRH_VEGFR2_9.pdb', 'docking_str/SRH_VEGFR2_10.pdb']   var sequences = ['GMWIMGRIP', 'VVWIMGRIP', 'KVWIMGRIP', 'FGYGIQYFM', 'INWIMGRIP', 'CLLVLSRGF', 'GMWVNSFGW', 'FGYGIQYRA', 'VVWVNSFGW', 'FGYGIQYGA']
   var energies = [-6.88, -6.24, -5.44, -4.99, -4.3, -3.72, -2.57, -2.53, -2.11, -1.46]
   peptide_reps = [];
    $(document).ready(function() {
      window.stage = new NGL.Stage("viewport",{ backgroundColor:"#FFFFFF" });
      window.stage.loadFile("docking_str/SRH_VEGFR2_1.pdb").then(function (nucl) {
        var aspectRatio = 2;
        var radius = 1.5;

        nucl.addRepresentation('cartoon', {
           "sele": ":A :E", "color": 0x94b4d1,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });
        nucl.addRepresentation('cartoon', {
           "sele": ":B :F", "color": 0x94d19c,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });
        nucl.addRepresentation('cartoon', {
           "sele": ":C :G", "color": 0xd6d989,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });
        nucl.addRepresentation('cartoon', {
           "sele": ":D :H", "color": 0xd98989,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });
        nucl.addRepresentation('cartoon', {
           "sele": "nucleic", "color": 0xd6d6d6,"aspectRatio":aspectRatio, "radius":radius,"radiusSegments":1,"capped":0 });
        nucl.addRepresentation('base', {
           "sele": "nucleic", "color": 0xd6d6d6});
        

        nucl.autoView();
      });

      var arrayLength = names.length;
      var k;
		for (k = 0; k < arrayLength; k++) {
            window.stage.loadFile(`${names[k]}`).then(function (nucl) {
                var repr = nucl.addRepresentation('hyperball', {
                   "sele": ":B", "color": 0xfc03ec});
                repr.setVisibility(false);
                peptide_reps.push(repr);
               
          	});
		}
    
    window.stage.viewerControls.spin( [ 0, 1, 0 ],110 )
    });
    var arrayLength = names.length;
			for (var i = 0; i < arrayLength; i++) {
        
        document.write(`<tr><td> <input type="checkbox" id="${i}" name="${sequences[i]}">  </td> <td> ${sequences[i]} </td> <td> ${energies[i]} </td></tr>`); 
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