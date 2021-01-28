## Welcome to Among Us Real Life

> Click to the button to join the game
> <a href="join.html">Join !</a>

<input id="playerName" type="text" placeholder="Entrez votre nom !"></input>
<button onclick="addPlayer();">Add Player</button>
<button onclick="launchGame();">Launch Game</button>

<script>

  players = [];

  function addPlayer()
  {
    var name = document.getElementById("playerName").value;
    players[players.length] = name;
  }

  function launchGame()
  {

    for (var i = 0; i < players.length; i++) {
      console.log(players[i]);
    }


  }


  console.log("Hello World");
</script>
