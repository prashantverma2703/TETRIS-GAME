Game is basically a collection of entities and infinite loop
where every time the loop is run the update and render function is called

Step 1: use the html canvas
	const canvas = document.getElementById('tetris');
	const context = canvas.getContext('2d'); 
//CONTEXT IS USED TO RETURN AN OBJECT WHICH GIVES ALL THE METHODS AND PROPERTIES TO DRAW LINES BOXED CIRCLES ETC IN CANVAS
	context.scale(20,20); //SCALE UP THE CANVAS(ZOOM)

Step 2: create array matrix with the shape of the tetris objects
	const matrix = [
	[0,0,0],
	[0,1,0],
	[1,1,1],
	];
Step 3: Create a function drawMatrix to create the playing object
	function drawMatrix(matrix,offset){
	forEach((row,y)=>{
	forEach((value,x)=>{
	if(value!==0){
	context.fillStyle= 'red';
	context.fllRect(x+offset,y+offset,1,1)
	}});});
// 1ST FOREACH LOOP SELECTS A ROW & OTHER FOREACH LOOP COMPARES EACH ELEMENT OF THE SELECTED ROW
IF THE VALUE IS 1 IN THE MATRIX IT IS PAINTED RED. 
IN context.fillRect X Y ARE  CORDINATED FOR LOCATION AND 1 1 ARE SIZE IN PIXEL.
SO OFFSET IS ADDED SO THAT THERE LOCATION CAN BE ALTERED WITH EVERY FUNCTION CALL.


Step 4: create an object 'player' with attributes as position and matrix, so that it can be passed as arguments to the drawMatrix.
	const player = {
	pos: {x:5,y:6},
	matrix:matrix,
	}
Step 5: Create a function 'draw' which calls the drawMatrix function with the player arguments.
	function draw(){
	drawMatrix(player.matrix,player.pos)
	}
Step 6: Create an update function so that the functions can be called continuously to display a motion
	function update(){
	draw();
	requestAnimationFrame(update);
	}
//window.requestAnimationFrame(); it makes sure after the rendering of one frame is completed the loop shoots up

Step 7: Copy the context.fillStyle & context.fillRect initial commands in side the draw function inorder to clear the place from where the object moves.

Step 8: Test the movement of object by changing player.pos.x & player.pos.y through consol.

Step 9: DROPPING THE OBJECT :
	PASS time=0 as an argument in the update function
	take a variable lasTime=0; 
	Inside update function :
	const deltaTime = time-lastTime;
	lastTime=time;
	// this will give incremental time;
	Introduce dropCounter =0 & drop Interval = 1000   (for milisecond)
	Now write
	dropCounter += deltaTime;
	if(dropCounter > dropInterval) {
	player.pos.y++;
	dropCounter=0;
	}
// this means when the dropcounter will become more than 1sec the object will come down by 1pixel.

Step 10: Moving left & right
	Add event listeners keydown, and increase and decrease the x cordinates using the keycodes of the left and right buttons in the if else loop.
	document.addEventListener('keydown', event=>{
	if(keycode===37)
	player.pos.x--;
	else if(keycode===39)
	player.pos.x++;
	});

Step 10.2 : declare another function called player drop, that pushes the object one 1block down when downkey is pressed.
	function playerDrop() {
	player.pos.y++;
	dropCounter = 0; // so that an interval is introduced.
 
Step 11: Now to map whole area into values of 0
	create a createMatrix function that takes width nad height as argument and a while loop is used until height is 0 , 0 is filled at every location.
	function createMatrix(w,h){
	while(h--){
	matrix.push(new Array(w).fill(0));
	}
	return matrix;
Step 12: create arena calling this function
	const arena = createMatrix(12,20);

Step 13: create a function merge that will copy all the player object matrix inside the arena.

Step 14: you can run the merge functionn in console, and consol,table(arena), to visualize the updated 0 to 1 

Step 15: COLLISION DETECTION


