# 3D-FPS-Shooting-Game
**DOOM** is a **3 dimensional first person shooter (FPS) shooting game** which uses the **raycasting algorithm** to generate a pseudo 3D environment and **pathfinding algorithm** for smart player enemy interaction. It is built using **Pygame** module in **Python** and takes advantage of the raycasting algorithm to make 3D gameplay despite not being a 3D game engine unlike Unity, Unreal, Godot, and others that are available in the market.

## Table of Contents

- [Player movement](#player-movement)
- [Raycasting Algorithm](#raycasting-algorithm)
- [Static and Animated Sprites (decorations)](#static-and-animated-sprites-decorations)
- [Weapon and shooting animation](#weapon-and-shooting-animation)
- [Player Enemy interaction (Pathfinding)](#player-enemy-interaction-pathfinding)
- [Enemies](#enemies)
- [Final Gameplay](#final-gameplay)
- [Installation](#How-to-run)

### Player movement
Initially, we built the player movements, which are based on any classic FPS shooting game, WASD keys for front, back, left, and right directions respectively, and left, and right arrow keys or mouse for the rotation of the player at that particular position.


### Raycasting algorithm
In the raycasting algorithm, I cast a fixed number of rays in the field of view of the player, if the field of view (FOV) angle is **X**, then the area visible to the player at a particular time would be equal to ***player's current angle (line of sight) - half of FOV angle (X/2)*** to ***player's current angle (line of sight) + half of FOV angle (X/2)***. The rays will be cast in this particular region till they meet an obstacle (wall) which will give the depth perspective of that particular point wrt the player. 

Once we get the collision point of the rays within the field of view (FOV) of the player, we can use it to generate a pseudo-3D perspective.
The current pseudo-3D looks even more realistic if we apply shaders to it, i.e. darkness of a particular point based on the distance of the collision point from the player (the farther the point, the darker the image). 

Now that we have obtained a pseudo-3D environment for our gameplay, we can add more life to it and make it look realistic by adding textures to the walls, adding a background and floor color.

### Static and Animated Sprites (decorations)
In order to make the game more beautiful we add static and animated sprites to make the game environment more realistic. The animated sprites are nothing but a collection of static images which are displayed on the screen faster than the human eye's persistence of vision which makes it look like it's a moving object, this can be achieved if the frame rate at which the images are displayed is faster than the persistence of vision of human eye, eg. 30 frames per second (fps), 60 fps, etc.

### Weapon and shooting animation
Now the game environment is achieved so we need to add a weapon and its shooting animation so that the player can interact with the enemies in the game. The shooting animation is triggered using the left mouse button which is accompanied with a waiting time for the recoil animation to get completed. Once the fire animation is complete the weapon is ready to shoot again.

### Player Enemy interaction (Pathfinding)
The first idea is that the enemy follows the player once the player is in line of sight and in a particular radius of the enemy. The enemy will try to follow the player along the line connecting the enemy and the player's current position keeping in mind the game environment constraints that the enemy cannot move outside the game screen and the enemy cannot move through walls. The implementation of this idea is given via the visual representation below (2D perspective to visualize the interaction properly).

The drawback of the above method is that the enemy tries to follow the player along the line connecting the enemy and the player, but when the player moves behind the wall the enemy tries to follow the player along the line through the wall but because of the presence of the wall is unable to do so, which looks stupid as we want our enemy to be smart and be able to navigate through the obstacles to reach the player through the shortest path possible. 

The enemy should be able to determine a workaround to reach the player once encountered with walls and this can be achieved via a pathfinding algorithm called breadth-first search (BFS).

### How to Run
- git clone https://github.com/Owen150/CG-Semester-Project.git
- cd Pygame-FPS
- python3 -m pip install -r requirements.txt
- python3 main.py
