## About The Zombie Challenge
This project tracks the movement of zombies over the grid and converts the creatures into zombies if they encounter the creatures on their path and newly created zombie will then start the movement in same path as original. This process continues until all zombies (initial + converted) finish their movement.

## Prerequisites:
- Java 8+
- Docker (not mandatory but good to have in order to run project with test cases without any hassle)

## How to run the project:
***With Docker***
- first, unzip the project if you already have zip bundle or clone the repository otherwise.
- go to project root folder after running below command

   ```sh
   cd ailo-zombie-challenge
   ```
- then, run below commands

   ```sh
   docker build -t ailo-zombie-challenge-kp .
   docker run ailo-zombie-challenge-kp
   ```

***Without Docker***
- go to project root folder and check for script file "run-zombie-challenge.sh" under script directory
- run below command
 
  ```
  sh run-zombie-challenge.sh
  ````

## How to observe output
Each test case output contains 3 seperate sections in console as asked in problem statement.
1. input
2. zombie movements
3. output

**for example,**

-------------- Inputs -------------
4
(3,1)
(0,1),(1,2),(1,1)
RDRU

----- Zombie Movements------
Zombie 0 moved to (0,1)
Zombie 0 infected creature at (0,1)
Zombie 0 moved to (0,2)
Zombie 0 moved to (1,2)
Zombie 0 infected creature at (1,2)
Zombie 0 moved to (1,1)
Zombie 0 infected creature at (1,1)
Zombie 1 moved to (1,1)

----------------------  OUTPUT  ----------------------
zombies' positions:
(1,1), (2,1), (3,1), (3,2)
creatures' positions:
none

## How to add custom test case
Test cases are written using JUnit test framework in source folder "test" using package com.test.ailo
If you want to test custom inputs beyond provided one, please add one or more test methods as below in class TestZombieChallenge.java under directory com/test/ailo in "test" folder.

**Reference method**

    @Test
	public void testCaseWhenCustomInput1() {
	    //defines input fields
		int gridSize = 4;
		int startX = 3, startY = 1;
		int[][] initCreaturePos = {{0,1}, {1,2}, {1,1}};
		List<String> zombiePaths = Arrays.asList("RDRU");
		
		//call real method
		Pair<List<Integer[]>, List<Integer[]>> result = 
				zombieChallenge.simulateMovements(gridSize, startX, startY, initCreaturePos, zombiePaths);
				
		//assert the result
		assertNotNull(result);
		
		List<Integer[]> zombiePositions = result.getItem1();
		List<Integer[]> creaturePositions = result.getItem2();
		
		//assert the size of final zombie positions in grid based on your input
		assertEquals(4, zombiePositions.size());
		assertEquals(0, creaturePositions.size());

        //assert the zombie positions with expected x,y co-ordinates based on your input
		TestUtils.assertList(zombiePositions, Arrays.asList(new Integer[] {1,1}, new Integer[] {2,1}, new Integer[] {3,2}, new Integer[] {3,1}));
	}

***Note*** : Above method is for reference, please change inputs and expected values to assert
