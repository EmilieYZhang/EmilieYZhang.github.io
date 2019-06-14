var canvas = document.getElementById("mazecanvas");
var context = canvas.getContext("2d");
var currRectX = 425;
var currRectY = 3;
var mazeWidth = 556;
var mazeHeight = 556;
var intervalVar;
var seconds = 300;
var endPoints = [
  [285, 55, 0],
  [385, 55, 0],
  [90, 35, 0],
  [385, 255, 0],
  [335, 90, 0],
  [235, 200, 0],
  [135, 240, 0],
  [410, 40, 0],
  [510, 135, 0],
  [150, 185, 0]//the points set the locations of each obstacles, or as the code calls it 'endpoints'
];

function createTimer() {
  intervalVar = setInterval(function () {
    makeWhite(mazeWidth, 0, canvas.width - mazeWidth, canvas.height);
    if (seconds === 0) {
      clearInterval(intervalVar);
      window.removeEventListener("keydown", moveRect, true);
      makeWhite(0, 0, canvas.width, canvas.height);
      context.font = "40px Arial";
      context.fillStyle = "red";
      context.textAlign = "center";
      context.textBaseline = "middle";
      context.fillText("Time's up!", canvas.width / 2, canvas.height / 2);
      return;
    }
    context.font = "20px Arial";
    if (seconds <= 10 && seconds > 5) {
      context.fillStyle = "orangered";
    }
    else if (seconds <= 5) {
      context.fillStyle = "red";
    }
    else {
      context.fillStyle = "purple";
    }
    context.textAlign = "center";
    context.textBaseline = "middle";
    var minutes = Math.floor(seconds / 60);
    var secondsToShow = (seconds - minutes * 60).toString();
    if (secondsToShow.length === 1) {
      secondsToShow = "0" + secondsToShow; // if the number of seconds is '5' for example, make sure that it is shown as '05'
    }
    context.fillText(minutes.toString() + ":" + secondsToShow, mazeWidth + 30, canvas.height / 2);
    seconds--;
  }, 1000);
}

window.addEventListener("keydown", moveRect, true); // added already
createTimer(); // add this line
// 120 seconds -> 2 minutes

function makeWhite(x, y, w, h) {
  context.beginPath();
  context.rect(x, y, w, h);
  context.closePath();
  context.fillStyle = "white";
  context.fill();
}

function makeHidden(x, y, w, h) {
  context.beginPath();
  context.rect(x, y, w, h);
  context.closePath();
  context.fillStyle = '#FEF5E7FB';
  context.fill();
  //this is the function to create a square around the character in order to hide the rest of the maze. This adds a level of difficulty for the player.
}

function drawMazeAndRectangle(rectX, rectY) {
  var mazeImg = new Image();
  mazeImg.src = "maze.gif";
  mazeImg.onload = function () { // when the image is loaded, draw the image, the rectangle and the circle
    makeWhite(0, 0, mazeImg.width, mazeImg.height + 20);

    context.drawImage(mazeImg, 0, 0);
    drawRectangle(rectX, rectY, "#0000FF", false, true);

    for (var t = 0; t < 10; t++) {
      context.beginPath();
      context.arc(endPoints[t][0], endPoints[t][1], 7, 0, 2 * Math.PI, false);
      context.closePath();
      if (endPoints[t][2] == 0) {
        context.fillStyle = '#00FF00';
      }
      else {
        context.fillStyle = '#BDC3C7';
      }
      context.fill();
    }

    makeHidden(0, 0, mazeImg.width, rectY - 50);
    makeHidden(0, rectY + 50, mazeImg.width, mazeImg.height);
    makeHidden(0, rectY - 50, rectX - 50, 100);
    makeHidden(rectX + 50, rectY - 50, mazeImg.width - (rectX - 50) - 100, 100);
  };
}

function drawRectangle(x, y, style) {
  makeWhite(currRectX, currRectY, 15, 15);
  currRectX = x;
  currRectY = y;
  context.beginPath();
  context.rect(x, y, 15, 15);
  context.closePath();
  context.fillStyle = style;
  context.fill();
}

function disableEndpoint(index) {

  context.beginPath();
  context.arc(endPoints[index][0], endPoints[index][1], 7, 0, 2 * Math.PI, false);
  context.closePath();
  context.fillStyle = '#BDC3C7';
  context.fill();

  endPoints[index][2] = 1;
}

drawMazeAndRectangle(52, 260);

function moveRect(e) {
  var newX;
  var newY;
  var canMove;
  e = e || window.event;
  switch (e.keyCode) {
    case 38:   // arrow up key
    case 87: // W key
      newX = currRectX;
      newY = currRectY - 5;
      break;
    case 37: // arrow left key
    case 65: // A key
      newX = currRectX - 5;
      newY = currRectY;
      break;
    case 40: // arrow down key
    case 83: // S key
      newX = currRectX;
      newY = currRectY + 5;
      break;
    case 39: // arrow right key
    case 68: // D key
      newX = currRectX + 5;
      newY = currRectY;
      break;
    default: return;
  }
  movingAllowed = canMoveTo(newX, newY);
  if (movingAllowed === 1) {      // 1 means 'the rectangle can move'
    drawMazeAndRectangle(newX, newY);
   
    currRectX = newX;
    currRectY = newY;
  }
  else if (movingAllowed === 2) { // 2 means 'the rectangle reached the end point'
    var endPointIndex = getEndPointIndex(newX, newY);
    disableEndpoint(endPointIndex);

    if (endPointIndex === 0) { // Q2 
      var answer = prompt("Question: What is the Capital of Canada?");
      if (answer == "Ottawa") {
        alert("correct!");
        drawMazeAndRectangle(285, 25);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(285, 25);
        //setInterval(seconds-20);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 1) { // Q2 
      var answerTwo = prompt("Question: What is 5 x 8?");
      if (answerTwo == "40") {
        alert("correct!");
        drawMazeAndRectangle(380, 70);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(380, 70);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 2) { // Q3
      var answerTwo = prompt("Question: What is the biggest animal in the world?");
      if (answerTwo == "Blue Whale" || answerTwo == "Whale") {
        alert("correct!");
        drawMazeAndRectangle(60, 30);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(60, 30);
        seconds = seconds - 20;
      }
    }

    else if (endPointIndex === 3) { // Q4
      var answerTwo = prompt("Question: What is the only mammal in the world that cannot jump?");
      if (answerTwo == "Elephant" || answerTwo == "elephant") {
        alert("correct!");
        drawMazeAndRectangle(345, 250);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(345, 250);
        seconds = seconds - 20;
      }
    }

    else if (endPointIndex === 4) { // Q5
      var answerTwo = prompt("Question: What is 6 x 5?");
      if (answerTwo == "30" || answerTwo == "Thirty") {
        alert("correct!");
        drawMazeAndRectangle(330, 80);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(330, 80);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 5) { // Q6
      var answerTwo = prompt("Question: What is 93 x 2");
      if (answerTwo == "186") {
        alert("correct!");
        drawMazeAndRectangle(235, 210);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(235, 210);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 6) { // Q7
      var answerTwo = prompt("Question: You are in a race. You pass the person in 2nd place, what place are you in now? First, Second, or Third?");
      if (answerTwo == "Second" || answerTwo == "Second place") {
        alert("correct!");
        drawMazeAndRectangle(135, 240);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(135, 240);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 7) { // Q8
      var answerTwo = prompt("Question: 48 + 17?");
      if (answerTwo == "65") {
        alert("correct!");
        drawMazeAndRectangle(410, 40);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(410, 40);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 8) { // Q9
      var answerTwo = prompt("Question: What is the country with the largest population in the world?");
      if (answerTwo == "China" || answerTwo == "china") {
        alert("correct!");
        drawMazeAndRectangle(510, 135);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(510, 135);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 9) { // Q10
      var answerTwo = prompt("Who is our Canadian Prime Minister? (Answer in full name)");
      if (answerTwo == "Justin Trudeau" || answerTwo == "justin trudeau") {
        alert("correct!");
        drawMazeAndRectangle(150, 185);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(150, 185);
        seconds = seconds - 20;
      }
    }

  }
}

window.addEventListener("keydown", moveRect, true);

function canMoveTo(destX, destY) {
  var imgData = context.getImageData(destX, destY, 15, 15);
  var data = imgData.data;
  var canMove = 1; // 1 means: the rectangle can move
  if (destX >= 0 && destX <= mazeWidth - 15 && destY >= 0 && destY <= mazeHeight - 15) { // check whether the rectangle would move inside the bounds of the canvas
    for (var i = 0; i < 4 * 15 * 15; i += 4) { // look at all pixels
      if (data[i] === 0 && data[i + 1] === 0 && data[i + 2] === 0) { // black
        canMove = 0; // 0 means: the rectangle can't move
        break;
      }
      else if (data[i] === 0 && data[i + 1] === 255 && data[i + 2] === 0) { // lime: #00FF00
        canMove = 2; // 2 means: the end point is reached
        break;
      }
    }
  }
  else {
    canMove = 0;
  }
  return canMove;
}

function getEndPointIndex(posX, posY) {
  var centerX = posX + 8;
  var centerY = posY + 8;
  var dx = 15;
  var dy = 15;

  for (var k = 0; k < 10; k++) {
    if ((centerX > (endPoints[k][0] - dx)) && (centerX < (endPoints[k][0] + dx)) && (centerY > (endPoints[k][1] - dy)) && (centerY < (endPoints[k][1] + dy))) {
      return k;
    }
  }

  return -1;
}
var canvas = document.getElementById("mazecanvas");
var context = canvas.getContext("2d");
var currRectX = 425;
var currRectY = 3;
var mazeWidth = 556;
var mazeHeight = 556;
var intervalVar;
var seconds = 300;
var endPoints = [
  [285, 55, 0],
  [385, 55, 0],
  [90, 35, 0],
  [385, 255, 0],
  [335, 90, 0],
  [235, 200, 0],
  [135, 240, 0],
  [410, 40, 0],
  [510, 135, 0],
  [150, 185, 0]
];

function createTimer() {
  intervalVar = setInterval(function () {
    makeWhite(mazeWidth, 0, canvas.width - mazeWidth, canvas.height);
    if (seconds === 0) {
      clearInterval(intervalVar);
      window.removeEventListener("keydown", moveRect, true);
      makeWhite(0, 0, canvas.width, canvas.height);
      context.font = "40px Arial";
      context.fillStyle = "red";
      context.textAlign = "center";
      context.textBaseline = "middle";
      context.fillText("Time's up!", canvas.width / 2, canvas.height / 2);
      return;
    }
    context.font = "20px Arial";
    if (seconds <= 10 && seconds > 5) {
      context.fillStyle = "orangered";
    }
    else if (seconds <= 5) {
      context.fillStyle = "red";
    }
    else {
      context.fillStyle = "purple";
    }
    context.textAlign = "center";
    context.textBaseline = "middle";
    var minutes = Math.floor(seconds / 60);
    var secondsToShow = (seconds - minutes * 60).toString();
    if (secondsToShow.length === 1) {
      secondsToShow = "0" + secondsToShow; // if the number of seconds is '5' for example, make sure that it is shown as '05'
    }
    context.fillText(minutes.toString() + ":" + secondsToShow, mazeWidth + 30, canvas.height / 2);
    seconds--;
  }, 1000);
}

window.addEventListener("keydown", moveRect, true); // added already
createTimer(); // add this line
// 120 seconds -> 2 minutes

function makeWhite(x, y, w, h) {
  context.beginPath();
  context.rect(x, y, w, h);
  context.closePath();
  context.fillStyle = "white";
  context.fill();
}

function makeHidden(x, y, w, h) {
  context.beginPath();
  context.rect(x, y, w, h);
  context.closePath();
  context.fillStyle = '#FEF5E7FB';
  context.fill();
}

function drawMazeAndRectangle(rectX, rectY) {
  var mazeImg = new Image();
  mazeImg.src = "maze.gif";
  mazeImg.onload = function () { // when the image is loaded, draw the image, the rectangle and the circle
    makeWhite(0, 0, mazeImg.width, mazeImg.height + 20);

    context.drawImage(mazeImg, 0, 0);
    drawRectangle(rectX, rectY, "#0000FF", false, true);

    for (var t = 0; t < 10; t++) {
      context.beginPath();
      context.arc(endPoints[t][0], endPoints[t][1], 7, 0, 2 * Math.PI, false);
      context.closePath();
      if (endPoints[t][2] == 0) {
        context.fillStyle = '#00FF00';
      }
      else {
        context.fillStyle = '#BDC3C7';
      }
      context.fill();
    }

    makeHidden(0, 0, mazeImg.width, rectY - 50);
    makeHidden(0, rectY + 50, mazeImg.width, mazeImg.height);
    makeHidden(0, rectY - 50, rectX - 50, 100);
    makeHidden(rectX + 50, rectY - 50, mazeImg.width - (rectX - 50) - 100, 100);
  };
}

function drawRectangle(x, y, style) {
  makeWhite(currRectX, currRectY, 15, 15);
  currRectX = x;
  currRectY = y;
  context.beginPath();
  context.rect(x, y, 15, 15);
  context.closePath();
  context.fillStyle = style;
  context.fill();
}

function disableEndpoint(index) {

  context.beginPath();
  context.arc(endPoints[index][0], endPoints[index][1], 7, 0, 2 * Math.PI, false);
  context.closePath();
  context.fillStyle = '#BDC3C7';
  context.fill();

  endPoints[index][2] = 1;
}

drawMazeAndRectangle(52, 260);

function moveRect(e) {
  var newX;
  var newY;
  var canMove;
  e = e || window.event;
  switch (e.keyCode) {
    case 38:   // arrow up key
    case 87: // W key
      newX = currRectX;
      newY = currRectY - 5;
      break;
    case 37: // arrow left key
    case 65: // A key
      newX = currRectX - 5;
      newY = currRectY;
      break;
    case 40: // arrow down key
    case 83: // S key
      newX = currRectX;
      newY = currRectY + 5;
      break;
    case 39: // arrow right key
    case 68: // D key
      newX = currRectX + 5;
      newY = currRectY;
      break;
    default: return;
  }
  movingAllowed = canMoveTo(newX, newY);
  if (movingAllowed === 1) {      // 1 means 'the rectangle can move'
    drawMazeAndRectangle(newX, newY);
    currRectX = newX;
    currRectY = newY;
  }
  else if (movingAllowed === 2) { // 2 means 'the rectangle reached the end point'
    var endPointIndex = getEndPointIndex(newX, newY);
    disableEndpoint(endPointIndex);

    if (endPointIndex === 0) { // Q2 
      var answer = prompt("Question: What is the Capital of Canada?");
      if (answer == "Ottawa") {
        alert("correct!");
        drawMazeAndRectangle(285, 25);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(285, 25);
        //setInterval(seconds-20);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 1) { // Q2 
      var answerTwo = prompt("Question: What is 5 x 8?");
      if (answerTwo == "40") {
        alert("correct!");
        drawMazeAndRectangle(380, 70);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(380, 70);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 2) { // Q3
      var answerTwo = prompt("Question: What is the biggest animal in the world?");
      if (answerTwo == "Blue Whale" || answerTwo == "Whale") {
        alert("correct!");
        drawMazeAndRectangle(60, 30);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(60, 30);
        seconds = seconds - 20;
      }
    }

    else if (endPointIndex === 3) { // Q4
      var answerTwo = prompt("Question: What is the only mammal in the world that cannot jump?");
      if (answerTwo == "Elephant" || answerTwo == "elephant") {
        alert("correct!");
        drawMazeAndRectangle(345, 250);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(345, 250);
        seconds = seconds - 20;
      }
    }

    else if (endPointIndex === 4) { // Q5
      var answerTwo = prompt("Question: What is 6 x 5?");
      if (answerTwo == "30" || answerTwo == "Thirty") {
        alert("correct!");
        drawMazeAndRectangle(330, 80);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(330, 80);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 5) { // Q6
      var answerTwo = prompt("Question: What is 93 x 2");
      if (answerTwo == "186") {
        alert("correct!");
        drawMazeAndRectangle(235, 210);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(235, 210);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 6) { // Q7
      var answerTwo = prompt("Question: You are in a race. You pass the person in 2nd place, what place are you in now? First, Second, or Third?");
      if (answerTwo == "Second" || answerTwo == "Second place") {
        alert("correct!");
        drawMazeAndRectangle(135, 240);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(135, 240);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 7) { // Q8
      var answerTwo = prompt("Question: 48 + 17?");
      if (answerTwo == "65") {
        alert("correct!");
        drawMazeAndRectangle(410, 40);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(410, 40);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 8) { // Q9
      var answerTwo = prompt("Question: What is the country with the largest population in the world?");
      if (answerTwo == "China" || answerTwo == "china") {
        alert("correct!");
        drawMazeAndRectangle(510, 135);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(510, 135);
        seconds = seconds - 20;
      }
    }
    else if (endPointIndex === 9) { // Q10
      var answerTwo = prompt("Who is our Canadian Prime Minister? (Answer in full name)");
      if (answerTwo == "Justin Trudeau" || answerTwo == "justin trudeau") {
        alert("correct!");
        drawMazeAndRectangle(150, 185);
      }
      else {
        alert("wrong!");
        drawMazeAndRectangle(150, 185);
        seconds = seconds - 20;
      }
    }

  }
}

window.addEventListener("keydown", moveRect, true);

function canMoveTo(destX, destY) {
  var imgData = context.getImageData(destX, destY, 15, 15);
  var data = imgData.data;
  var canMove = 1; // 1 means: the rectangle can move
  if (destX >= 0 && destX <= mazeWidth - 15 && destY >= 0 && destY <= mazeHeight - 15) { // check whether the rectangle would move inside the bounds of the canvas
    for (var i = 0; i < 4 * 15 * 15; i += 4) { // look at all pixels
      if (data[i] === 0 && data[i + 1] === 0 && data[i + 2] === 0) { // black
        canMove = 0; // 0 means: the rectangle can't move
        break;
      }
      else if (data[i] === 0 && data[i + 1] === 255 && data[i + 2] === 0) { // lime: #00FF00
        canMove = 2; // 2 means: the end point is reached
        break;
      }
    }
  }
  else {
    canMove = 0;
  }
  return canMove;
}

function getEndPointIndex(posX, posY) {
  var centerX = posX + 8;
  var centerY = posY + 8;
  var dx = 15;
  var dy = 15;

  for (var k = 0; k < 10; k++) {
    if ((centerX > (endPoints[k][0] - dx)) && (centerX < (endPoints[k][0] + dx)) && (centerY > (endPoints[k][1] - dy)) && (centerY < (endPoints[k][1] + dy))) {
      return k;
    }
  }

  return -1;
}
