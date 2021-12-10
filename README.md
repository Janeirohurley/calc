# calc

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" type="text/css" href="style.css">
    <script src="script.js"></script>
    <style type="text/css">
    body {
    font-family: 'Open Sans', sans-serif;
    margin: 0;
    }
    #result {
    height: 120px;
    }
    
    #history {
    text-align: right;
    height: 20px;
    margin: 0 20px;
    padding-top: 20px;
    font-size: 15px;
    color: #919191;
    }
    
    #output {
    text-align: right;
    height: 60px;
    margin: 10px 20px;
    font-size: 30px;
    }
    
    #keyboard {
    height: 400px;
    }
    
    .operator, .number, .empty {
    width: 50px;
    height: 50px;
    margin: 15px;
    float: left;
    border-radius: 50%;
    border-width: 0;
    font-weight: bold;
    font-size: 15px;
    }
    
    .number, .empty {
    background-color: #c4e5fa;
    }
    
    .number, .operator {
    cursor: pointer;
    }
    
    .operator:active, .number:active {
    font-size: 13px;
    }
    
    .operator:focus, .number:focus, .empty:focus {
    outline: 0;
    }
    
    button:nth-child(4) {
    font-size: 20px;
    background-color: #20b2aa;
    outline:none;
    }
    
    button:nth-child(8) {
    font-size: 20px;
    background-color: #66ec18;
    }
    
    button:nth-child(12) {
    font-size: 20px;
    background-color: #f08080;
    }
    
    button:nth-child(16) {
    font-size: 20px;
    background-color: #f1bc0e;
    }
    
    button:nth-child(20) {
    font-size: 20px;
    background-color: #9477af;
    }
    
    
    </style>
    <title>Calculator</title>
</head>
<body>
    <div id="container">
    <div id="calculator">
    <div id="result">
    <div id="history">
    <p id="history-value"></p>
    </div>
    <div id="output">
    <p id="output-value"></p>
    </div>
    </div>
    <div id="keyboard">
    <button class="operator" id="clear">C</button>
    <button class="operator" id="backspace">CE</button>
    <button class="operator" id="%">%</button>
    <button class="operator" id="/">&#247;</button>
    <button class="number" id="7">7</button>
    <button class="number" id="8">8</button>
    <button class="number" id="9">9</button>
    <button class="operator" id="*">&times;</button>
    <button class="number" id="4">4</button>
    <button class="number" id="5">5</button>
    <button class="number" id="6">6</button>
    <button class="operator" id="-">-</button>
    <button class="number" id="1">1</button>
    <button class="number" id="2">2</button>
    <button class="number" id="3">3</button>
    <button class="operator" id="+">+</button>
    <button class="empty" id="empty"></button>
    <button class="number" id="0">0</button>
    <button class="empty" id="empty"></button>
    <button class="operator" id="=">=</button>
    </div>		
    </div>
    </div>
    <script type="text/javascript">//Function to get History
    function getHistory(){
    return document.getElementById("history-value").innerText;
    }
    //Print History Value
    function printHistory(num){
    document.getElementById("history-value").innerText=num;
    }
    //Get Output Value
    function getOutput(){
    return document.getElementById("output-value").innerText;
    }
    //Print Output Value
    function printOutput(num){
    if(num==""){
    document.getElementById("output-value").innerText=num;
    }
    else{
    document.getElementById("output-value").innerText=getFormattedNumber(num);
    }	
    }
    //Get formatted number
    function getFormattedNumber(num){
    if(num=="-"){
    return "";
    }
    var n = Number(num);
    var value = n.toLocaleString("en");
    return value;
    }
    //Reverse Number format
    function reverseNumberFormat(num){
    return Number(num.replace(/,/g,''));
    }
    var operator = document.getElementsByClassName("operator");
    for(var i =0;i<operator.length;i++){
    operator[i].addEventListener('click',function(){
    if(this.id=="clear"){
    printHistory("");
    printOutput("");
    }
    else if(this.id=="backspace"){
    var output=reverseNumberFormat(getOutput()).toString();
    if(output){//if output has a value
    output= output.substr(0,output.length-1);
    printOutput(output);
    }
    }
    else{
    var output=getOutput();
    var history=getHistory();
    if(output==""&&history!=""){
    if(isNaN(history[history.length-1])){
    history= history.substr(0,history.length-1);
    }
    }
    if(output!="" || history!=""){
    output= output==""?output:reverseNumberFormat(output);
    history=history+output;
    if(this.id=="="){
    var result=eval(history);
    printOutput(result);
    printHistory("");
    }
    else{
    history=history+this.id;
    printHistory(history);
    printOutput("");
    }
    }
    }
    
    });
    }
    var number = document.getElementsByClassName("number");
    for(var i =0;i<number.length;i++){
    number[i].addEventListener('click',function(){
    var output=reverseNumberFormat(getOutput());
    if(output!=NaN){ //if output is a number
    output=output+this.id;
    printOutput(output);
    }
    });
    }</script>
</body>
</html>

