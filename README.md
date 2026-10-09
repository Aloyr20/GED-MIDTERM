##  GED-MIDTERM

# Reference: I used the Jump Method and the Base Movement types from the MarioController, The Singleton Base Class code and ScoreCounter code all from In-Class-Activity-2 && Lab Assignment #1. The Singleton Base Class code from that was from Lecture 3: Design Patterns
https://github.com/Aloyr20/In-Class-Activities-GED.git

# Brief Overview

For the practical portion of the midterm I was tasked with creating a small prototype version of Bubble Bobble. I was able to create a basic PlayerController script that allows the character to move left and right and jump. Using the singleton base class I also implemented a Singleton-based score system that stores a shared score, has methods to add score, remove score and reset score and its able to update the UI display of the score itself.

<img width="1001" height="570" alt="{98BC8DAB-9708-4E69-8274-FB8302A6C64D}" src="https://github.com/user-attachments/assets/3ad4c28c-36eb-41bb-8687-ddb92ecb3eaa" />

# How I Implemented Object Oriented Programming

## Encapsulation

I used Encapsulation by keeping the score private inside of ScoreCounter and then I have methods inside of ScoreCounter which can add score, remove score, reset the score so other scripts can still retrieve it and change it by calling the method. The player movement settings like the are also private however they are SerializeFields making them adjustable via the inspector in unity. 

I did this so that an object could add score using the AddScore() method without directly needing to access the value of the score itself. Keeping things like the Score private, prevent it from being changed or altered accidently by other scripts directly, while still giving the ability for the score to be changed through methods like AddScore() when called upon by another script. SerializeFields for player movement settings like speed and jump force allow for them to be altered in the inspector while keeping them protected from being change by other scripts unintentionally.

## Inheritance

I used Inheritance for the ScoreCounter as it inherits from Singleton<ScoreCounter> and it reuses the Singleton<T> base classes code of making sure only one shared ScoreCounter instance exists and removing duplicates if another does exist. The ScoreCounter overrides the Awake method from Singleton<ScoreCounter> and calls base.Awake() before the score display is initalized.

I did this so that I reduce the amount of duplicated code and so that the Singleton initialization itself is separate from the actual system that controls the score.

## Composition

I used composition through the PlayerController script since the players behaviour works by combining multiple different components together. The PlayerController script reads input and uses Transform for the player movement and Rigidbody2D so that the player can jump.

I did this so that each component of the player handles specific responsibilities while keeping it easy to manage and modify accordingly. As an example, if I wanted to adjust how the player falls without having to modify the input handling I can just adjust the gravity of the Rigidbody2D. 

# How I Implemented The Singleton Pattern

## Singleton

I implemented the Singleton pattern through the Singleton<T> base class which was shown in class so that their would be a single Score counter managing the score for the whole game without needing to set up other game objects/score systems in other scenes of the game. You access score counter through ScoreCounter.Instance. 

I used this so that different gameplay objects could contribute to the same score without having to create seperate counters.   

# How I Would've Implemented The Factory Pattern

## Factory

If I was able to create something using a factory pattern in relation to the game I would've made a Factory Method to create two different bubble types one being a bubble that freely moves around and one being a bubble containing a trapped enemy. 

Both types would inherit from a Bubble base class with common movement and popping methods. A BubbleFactory would have a CreateBubble(), which FreeMovingBubbleFactory and the TrappedEnemyBubbleFactory would then override to create either a bubble that freely moves or a bubble that contains a trapped enemy. 

When the player would have blowed a bubble, FreeBubbleFactory would've created it. When it wouldve traped an enemy, TrappedBubble would've then created a replacement bubble that contained a reference to the enemy that was trapped. Once the bubble was popped, I would've made it so it defeated the enemy and added score through the existing ScoreCounter.Instance.AddScore() method.

I would've used a factory here so that I could separate the bubble creation itself from the PlayerController. The Factory would handle the creating of each bubble type while the player and any other scripts would request a bubble type. This would make it easier to modify the bubble creation in the future as the creation would be handled separately. 
