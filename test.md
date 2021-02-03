## Welcome to Among Us Real Life

> Click to the button to join the game
> <a href="join.html">Join !</a>

<select id="impostor" name="impostor">
  <option default value="1">1</option>
  <option value="2">2</option>
  <option value="3">3</option>
  <option value="4">4</option>
  <option value="5">5</option>
  <option value="6">6</option>
  <option value="7">7</option>
  <option value="8">8</option>
  <option value="9">9</option>
</select>

<select id="sherif" name="sherif">
  <option default value="0">0</option>
  <option value="1">1</option>
</select>

<input id="playerName" type="text" placeholder="Entrez votre nom !">
<button class="btn btn-github" onclick="addPlayer();">Add Player</button>
<button class="btn btn-github" onclick="launchGame();">Launch Game</button>

<script>

  players = [];
  impostors = [];
  impIndex = [];
  sherifIndex = -1;


  function addPlayer()
  {
    var name = document.getElementById("playerName").value;
    players[players.length] = name;
    document.getElementById("playerName").value = "";
  }

  //Lancer le jeu
  function launchGame()
  {

    for (var i = 0; i < players.length; i++) {
      console.log(players[i]);
    }

    impostors = getImpostors();
    //var sherif = getSherif();
  }

  function getSherif()
  {
    //getRandomInt
    var count = parseInt(document.getElementById("sherif").value);

    var crewmateList = [];
    for(var i = 0; i < players.length; i++)
    {
      var isImpostor = false;
      for(var j = 0; j < impIndex.length; j++)
      {
        console.log("Sherif Test "+ i + " == "+ impIndex[j]);
        if(i == impIndex[j])
        {
          isImpostor = true;
        }
      }
      if(!isImpostor)
      {
        crewmateList[crewmateList.length] = i;
      }
    }



    if(count > 0)
    {
      sherifIndex = crewmateList[getRandomInt(0, crewmateList.length-1)];
    }

    console.log("------ Sherif ------");
    //for (var i = 0; i < impIndex.length; i++) {
    if(count > 0){
      console.log(players[sherifIndex] + " " + sherifIndex);
    }
    //}
    console.log("-----------------------");




    nextCrewmate(0);
  }

  function getImpostors()
  {
    var count = getImpCount();


    var index = 0;
    var min = 0;
    var max = players.length / count;
    var _max = max;
    while(index < count){


      impIndex[impIndex.length] = getRandomInt(min, max-1);


      min = max + 1;
      max = min+(_max-1);//(max * (index+1)) - 1;
      index++;
    }
    console.log("------ Impostors ------");
    for (var i = 0; i < impIndex.length; i++) {
      console.log(players[impIndex[i]] + " - " + impIndex[i]);
    }
    console.log("-----------------------");
    getSherif();
  }

  function nextCrewmate(index)
  {

    var playerName = players[index];
    var isStartGame = (playerName == null);

    if(isStartGame)
    {
    playerName = "Bonne partie !";
    }

    var code = "<p>"+playerName +"</p>";
    if(!isStartGame){
      code += "<button class=\"btn btn-github\" onclick=\"showTeam("+ index+");\">Continue</button>";
    } else {
      code += "<button class=\"btn btn-github\" onclick=\"showButton();\">Launch Game !</button>";
    }


    document.getElementsByTagName("body")[0].innerHTML = code;
  }
  function showButton(){

    var code = "<button class="btn btn-github" onclick="addPlayer();"><img src=\"au_btn.png\" ></button>";


    document.getElementsByTagName("body")[0].innerHTML = code;
  }

  function showTeam(index)
  {
    var playerName = players[index];
    var team = "Crewmate";

    var impostorList = "";

    for (var i = 0; i < impIndex.length; i++) {
      impostorList += " "+players[impIndex[i]]+" ";
      console.log("("+impIndex[i]+" == "+index+")");
      if(impIndex[i] == index)
      {
        team = "Impostor";
      }
    }

    if(index == sherifIndex)
    {
      team = "Sherif";
    }

    if(team == "Impostor")
    {
      team += "("+impostorList+")";
    }


    if(players.length > index)
    {
      var code = "<p>"+playerName + " - "+ team+"</p>";
      code += "<button class=\"btn btn-github\" onclick=\"nextCrewmate("+ (index+1) +");\">Continue</button>";



      document.getElementsByTagName("body")[0].innerHTML = code;

    }
  }

  function getImpCount()
  {
    return parseInt(document.getElementById("impostor").value);
  }

  function getRandomInt(min, max) {
  min = Math.ceil(min);
  max = Math.floor(max);
  return Math.floor(Math.random() * (max - min)) + min;
}


  console.log("Sherif Update (3)");
</script>
