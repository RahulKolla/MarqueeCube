#Rahul Kolla
#October 20, 2021
#Homework 4: MMIO with Mars
#Absolute Constants 
.eqv WIDTH 64
.eqv HEIGHT 64
#Colors the program uses
.eqv	RED 	0x00FF0000
.eqv	GREEN 	0x0000FF00
.eqv	BLUE	0x000000FF
.eqv	WHITE   0x00FFFFFF
.eqv	YELLOW	0x00FFFF00
.eqv	CYAN	0x0000FFFF
.eqv	MAGENTA	0x00FF00FF
.eqv	BLACK	0x00000000

.data
#Color arrays that we cycle through for the marquee affect
colors: .word 	RED, GREEN, BLUE, WHITE, YELLOW, CYAN, MAGENTA
colors2: .word 	GREEN, BLUE, WHITE, YELLOW, CYAN, MAGENTA, RED
colors3: .word 	BLUE, WHITE, YELLOW, CYAN, MAGENTA, RED, GREEN
colors4: .word 	WHITE, YELLOW, CYAN, MAGENTA, RED, GREEN, BLUE
colors5: .word 	YELLOW, CYAN, MAGENTA, RED, GREEN, BLUE, WHITE
colors6: .word 	CYAN, MAGENTA, RED, GREEN, BLUE, WHITE, YELLOW
colors7: .word  MAGENTA, RED, GREEN, BLUE, WHITE, YELLOW, CYAN
colors8: .word  BLACK, BLACK, BLACK, BLACK, BLACK, BLACK, BLACK
#loadable constants that we modify throughout the program
width: .word	64
height: .word 	64

.text
main:
	#our default color array
	la	$t5, colors
	lw 	$a2, ($t5)
	#this is the constant that regulates our color array
	li	$t6, 0
	#these are the variables we use to manipulate the position of the box
	lw	$s0, width
	lw 	$s1, height
	#setting up our variables with 64
	add 	$a0, $0, $s0    
	sra 	$a0, $a0, 1  
	add 	$a1, $0, $s0   
	sra 	$a1, $a1, 1
	#t2 is the operator that becomes our counter within these loops
	li	$t2, 0
	#t3 is the operator that is our termination condition within these loops
	li	$t3, 7

loop:
	#draws our inital box
	jal	drawBox
	# check for input
	lw $t0, 0xffff0000  
	#if no input we loop back
    	beq $t0, 0, loop   
	# process input with if statements
	lw 	$s2, 0xffff0004
	beq	$s2, 32, exit	# input space
	beq	$s2, 119, up 	# input w
	beq	$s2, 115, down 	# input s
	beq	$s2, 97, left  	# input a
	beq	$s2, 100, right	# input d
	# invalid input, ignore
	j	loop
	
exit:	
	#exit condition
	li	$v0, 10
	syscall

black:
	#inaccessible by the normal box and is only called upon when we need to set the box to black 
	#this is to allow the new box to come to fruition 
	#la	$t5, colors8
	#lw 	$a2, ($t5)
	
drawBox:
topRow:	
	#DELAY CONDITION - SLOWS PROGRAM DOWN BUT CAN BE INCLUDED WHICH MAKES THE BOX DRAW SLOW
	#PREFERED USAGE IS THIS BEING COMMENTED OUT BUT NOT COMMENTED OUT TO FIT THE PROGRAM REQUIREMENTS 
	li	$v0, 32
	li	$a3, 5
	syscall
	#WE USE THE STACK HERE TO CYCLE THROUGH EACH BIT BY PUSHING AND POPING
	addi	$sp, $sp, -4
	sw      $ra, ($sp)
	#Jump and link to our draw pixel function
	jal 	draw_pixel
	lw	$ra, ($sp)
	addi	$sp, $sp, 4
	#we increment a0 by one to draw the next pixel at this location (1 right)
	addi	$a0, $a0, 1
	#cycles to the next color within our color array
	lw 	$a2, ($t5)
	addi	$t5, $t5, 4
	#increments our counter by 1
	addi	$t2, $t2, 1
	#the moment our counter hits the termination number we jump to reset colors
	bge 	$t2, $t3, resetColors
	#otherwise we jump to the top of the loop
	j	topRow
	
resetColors:
	#depending on what our t6 (our color controller) variable is we load in that specific array
	beq	$t6, 7, a7
	beq	$t6, 6, a6
	beq	$t6, 5, a5
	beq	$t6, 4, a4
	beq	$t6, 3, a3
	beq	$t6, 2, a2
	beq	$t6, 1, a1
	beq	$t6, 0, a
a: 
	#controls our default array
	la	$t5, colors
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array
a1: 
	#controls our second array
	la	$t5, colors2
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array
a2: 
	#controls our third array
	la	$t5, colors3
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array

a3: 
	#controls our fourth array
	la	$t5, colors4
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array

a4: 
	#controls our fifth array
	la	$t5, colors5
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array
	
a5: 
	#controls our sixth array
	la	$t5, colors6
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array

a6: 
	#controls our seventh array
	la	$t5, colors7
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array
	
a7: 
	#controls our BLACK array
	la	$t5, colors8
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	rightCol #We jump to right column after setting the array
	
rightCol:
	#DELAY CONDITION - SLOWS PROGRAM DOWN BUT CAN BE INCLUDED WHICH MAKES THE BOX DRAW SLOW
	#PREFERED USAGE IS THIS BEING COMMENTED OUT BUT NOT COMMENTED OUT TO FIT THE PROGRAM REQUIREMENTS 	
	li	$v0, 32
	li	$a3, 5
	syscall
	#WE USE THE STACK HERE TO CYCLE THROUGH EACH BIT BY PUSHING AND POPING
	addi	$sp, $sp, -4
	sw      $ra, ($sp)
	#Jump and link to our draw pixel function
	jal 	draw_pixel
	lw	$ra, ($sp)
	addi	$sp, $sp, 4
	#we increment a1 by one to draw the next pixel at this location (1 down)
	addi	$a1, $a1, 1
	#cycles to the next color within our color array
	addi	$t5, $t5, 4
	lw 	$a2, ($t5)
	#increments our counter by 1
	addi	$t2, $t2, 1
	#the moment our counter hits the termination number we jump to reset colors
	beq	$t2, $t3, resetColors2
	#otherwise we jump to the top of the loop
	j	rightCol

resetColors2:
	#depending on what our t6 (our color controller) variable is we load in that specific array
	beq	$t6, 7, b7
	beq	$t6, 6, b6
	beq	$t6, 5, b5
	beq	$t6, 4, b4
	beq	$t6, 3, b3
	beq	$t6, 2, b2
	beq	$t6, 1, b1
	beq	$t6, 0, b0
	
b0: 
	#controls our default array
	la	$t5, colors
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array
b1: 
	#controls our second array
	la	$t5, colors2
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array
b2: 
	#controls our third array
	la	$t5, colors3
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array

b3: 
	#controls our fourth array
	la	$t5, colors4
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array

b4: 
	#controls our fifth array
	la	$t5, colors5
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array
	
b5: 
	#controls our sixth array
	la	$t5, colors6
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array

b6: 
	#controls our seventh array
	la	$t5, colors7
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array

b7:
	#controls our BLACK array
	la	$t5, colors8
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	bottomRow #We jump to bottom row after setting the array
	
bottomRow:
	#DELAY CONDITION - SLOWS PROGRAM DOWN BUT CAN BE INCLUDED WHICH MAKES THE BOX DRAW SLOW
	#PREFERED USAGE IS THIS BEING COMMENTED OUT BUT NOT COMMENTED OUT TO FIT THE PROGRAM REQUIREMENTS 	
	li	$v0, 32
	li	$a3, 5
	syscall
	#WE USE THE STACK HERE TO CYCLE THROUGH EACH BIT BY PUSHING AND POPING
	addi	$sp, $sp, -4
	sw      $ra, ($sp)
	#Jump and link to our draw pixel function
	jal 	draw_pixel
	lw	$ra, ($sp)
	addi	$sp, $sp, 4
	#we decrement a0 by one to draw the next pixel at this location (left of one)
	addi	$a0, $a0, -1
	#cycles to the next color within our color array
	addi	$t5, $t5, 4
	lw 	$a2, ($t5)
	#increments our counter by 1
	addi	$t2, $t2, 1
	#the moment our counter hits the termination number we jump to reset 
	beq	$t2, $t3, resetColors3
	j	bottomRow

resetColors3:
	#depending on what our t6 (our color controller) variable is we load in that specific array
	beq	$t6, 7, c7
	beq	$t6, 6, c6
	beq	$t6, 5, c5
	beq	$t6, 4, c4
	beq	$t6, 3, c3
	beq	$t6, 2, c2
	beq	$t6, 1, c1
	beq	$t6, 0, c0
	
c0: 
	#controls our default array
	la	$t5, colors
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array
c1: 
	#controls our second array
	la	$t5, colors2
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array
c2: 
	#controls our third array
	la	$t5, colors3
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array

c3: 
	#controls our fourth array
	la	$t5, colors4
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array

c4: 
	#controls our fifth array
	la	$t5, colors5
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array
	
c5: 
	#controls our sixth array
	la	$t5, colors6
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array

c6:  
	#controls our seventh array
	la	$t5, colors7
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array

c7: 
	#controls our BLACK array
	la	$t5, colors8
	lw 	$a2, ($t5)
	li	$t2, 0
	j 	leftCol #We jump to left column after setting the array
	
leftCol:
	#DELAY CONDITION - SLOWS PROGRAM DOWN BUT CAN BE INCLUDED WHICH MAKES THE BOX DRAW SLOW
	#PREFERED USAGE IS THIS BEING COMMENTED OUT BUT NOT COMMENTED OUT TO FIT THE PROGRAM REQUIREMENTS 	
	li	$v0, 32
	li	$a3, 5
	syscall	
	#WE USE THE STACK HERE TO CYCLE THROUGH EACH BIT BY PUSHING AND POPING
	addi	$sp, $sp, -4
	sw      $ra, ($sp)
	#Jump and link to our draw pixel function
	jal 	draw_pixel
	lw	$ra, ($sp)
	addi	$sp, $sp, 4
	#we decrement a1 by one to draw the next pixel at this location (up one)
	addi	$a1, $a1, -1
	#cycles to the next color within our color array
	addi	$t5, $t5, 4
	lw 	$a2, ($t5)
	#increments our counter by 1
	addi	$t2, $t2, 1
	#the moment our counter hits the termination number we jump to reset 
	beq	$t2, $t3, temp
	j 	leftCol
	
temp:
	#depending on what our t6 (our color controller) variable is we load in that specific array
	beq	$t6, 7, color7
	beq	$t6, 6, color6
	beq	$t6, 5, color5
	beq	$t6, 4, color4
	beq	$t6, 3, color3
	beq	$t6, 2, color2
	beq	$t6, 1, color1
	beq	$t6, 0, color
	
startPoint:	
	#reset the counter here
	li	$t2, 0
	#reseting the a0 variable back to zero (x coordinate)
	add 	$a0, $0, $0    
	#reseting the a1 variable back to zero (x coordinate)
	add 	$a1, $0, $0    
	#setting to whatever s0 is depending on the movement
	add	$a0, $0, $s0   
	sra 	$a0, $a0, 1
	#setting to whatever s1 is depending on the movement
	add	$a1, $0, $s1   
	sra 	$a1, $a1, 1
	#return to the function that called it
	jr	$ra
	
color7:
	#our blacked array set
	la	$t5, colors8
	lw 	$a2, ($t5)
	subi 	$t6, $t6, 7
	j	startPoint
	
color6:
	#our seventh array set
	la	$t5, colors7
	lw 	$a2, ($t5)
	subi 	$t6, $t6, 6
	j	startPoint
	
color5:
	#our sixth array set
	la	$t5, colors6
	lw 	$a2, ($t5)
	addi	$t6, $t6, 1
	j	startPoint

color4:
	#our fifth array set
	la	$t5, colors5
	lw 	$a2, ($t5)
	addi	$t6, $t6, 1
	j	startPoint
	
color3:
	#our fourth array set
	la	$t5, colors4
	lw 	$a2, ($t5)
	addi 	$t6, $t6, 1
	j	startPoint
	
color2:
	#our third array set
	la	$t5, colors3
	lw 	$a2, ($t5)
	addi	$t6, $t6, 1
	j	startPoint

color1:
	#our second array set
	la	$t5, colors2
	lw 	$a2, ($t5)
	addi	$t6, $t6, 1
	j	startPoint
	
color:
	#our default array set
	la	$t5, colors
	lw 	$a2, ($t5)
	addi 	$t6, $t6, 1
	j	startPoint
	
# $a0 = X
# $a1 = Y
# $a2 = color
draw_pixel:
	# s1 = address = $gp + 4*(x + y*width)
	mul	$t9, $a1, WIDTH   # y * WIDTH
	add	$t9, $t9, $a0	  # add X
	mul	$t9, $t9, 4	  # multiply by 4 to get word offset
	add	$t9, $t9, $gp	  # add to base address
	sw	$a2, ($t9)	  # store color at memory location
	jr 	$ra
	
up:	#our up function
	li	$t6, 7		# black out the pixel
	jal	black		#calls the black function to black out the og box
	addi	$s1, $s1, -2	#shifts the y coordinate up one
	jal	startPoint	#draws the new box
	j	loop		#goes back to the loop

down:	#our down function
	li	$t6, 7		# black out the pixel
	jal	black 		#calls the black function to black out the og box
	addi	$s1, $s1, 2	#shifts the y coordinate down one
	jal	startPoint	#draws the new box
	j	loop		#goes back to the loop
	
left:	#our left function
	li	$t6, 7		#black out the pixel
	jal	black		#calls the black function to black out the og box
	addi	$s0, $s0, -2	#shifts the x coordinate left one
	jal	startPoint	#draws the new box
	j	loop		#goes back to the loop
	
right:	#our right function 
	li	$t6, 7		# black out the pixel
	jal	black		#calls the black function to black out the og box
	addi	$s0, $s0, 2	#shifts the x coordinate right one
	jal	startPoint	#draws the new box
	j	loop		#goes back to the loop
