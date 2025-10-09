# FOP Valley

All the resources mentioned in this assignment can be found at [Here](https://github.com/funteck123/FOP_Tron/tree/main).

As of your Fundamental of Programming (FOP) Assignment, you are required to design and develop a 2D interactive game inspired by the Tron: Legacy (2010) and [Tron (1982 movie and video game)](https://en.wikipedia.org/wiki/Tron_(video_game)).

## 1 - Introduction

![A Slime](image/slime.png)

In this assignment, your task is to create a 2D interactive arena game that combines strategic gameplay with narrative storytelling. Players will control a futuristic Light Cycle that leaves behind a glowing energy trail (jetwall) as it moves through the Grid. The goal is simple — outmaneuver your opponents and make them collide with jetwalls, walls, or each other to be the last cycle standing.

However, this is not merely a game about survival. You are also tasked to implement an underlying storyline system, where narrative elements and cutscenes based on the Tron universe are progressively revealed through gameplay. Players will unlock new story chapters, achievements, and characters as they level up.

Your project should strike a balance between story progression and gameplay mechanics — approximately half the focus on player experience and narrative flow, and the other half on AI logic, collision systems, and technical implementation.

## 2 - Basic Requirement (Total - 8 marks)

### 2.1 Arena Design (0.5 mark)

* Design a **40x40 grid-based arena** that represents the Light Cycle battlefield.
* Players must be able to move their cycles using the **W, A, S, and D keys**:
    * `W` moves upward
    * `S` moves downward
    * `A` moves left
    * `D` moves right
* Each cycle leaves behind a **jetwall** that acts as an impassable barrier.
* Hitting a jetwall or boundary wall causes the player to lose half a life (**-0.5 HP**) instead of instant derezzing.
* However, if the arena is an **open-type grid** (no boundaries), falling off results in the loss of all remaining lives.
* Provide **three predesigned arenas** and **one randomly generated arena** option.
* These arenas can differ in layout, speed ramp placement, and obstacle arrangement.


### 2.2 - Creating characters (1 marks)

#### 2.2.1 Create 5 archetypes

1. Create two character classes based on the information provided in `characters.txt`. This file contains the names of characters along with their initial attributes, including `speed`, `handling`, `lives`, 'discsOwned' and `experiencePoints`. When a player creates a new character, the character's initial attributes should be determined by the data in `character.txt`.

2. `Characters` class should include a method called `levelUp()`.

3. Incorporate the principles of OOP. For instance, you can structure your code as follows in Java:

```java
class Tron extends Character {
    // Define instance variables here
}
```

Each playable character offers a distinct experience. 

Character	Color	Speed	Handling	Description Playable
Tron	Blue	High	Balanced	The original defender of the Grid. Yes
Kevin Flynn	White	Moderate	Smooth	The creator — stable and resilient. Yes

Both characters share core properties such as speed, handling, lives, discsOwned, and experiencePoints. As they level up, their performance improves and new features such as light cycle variants, cutscenes, or storyline branches can be unlocked.

Archetype data should be loaded from a file (archetypes.txt) using File I/O.
 No marks will be awarded if values are hardcoded without demonstrating file handling.


#### 2.2.2 Implement leveling-up system

As characters progress through the Grid, they can gain experience (XP) and level up.
Here are the general rules for progression:

- During the first 10 levels, characters will require fewer experience points to level up, allowing for rapid early advancement.
- Defeating enemy Light Cycles awards XP based on their difficulty.
- Each level grants:
    - Improved speed or turn rate.
    - +1 life every 10 levels.
    - Additional disc slot every 15 levels.
    - Unlocks of new playable characters and story chapters.
- Maximum attainable level: 99.
- The rate of attribute increase upon leveling up will vary based on the character type:
  - `Tron`: Gains more speed and stability per level.
  - `Kevin Flynn`: Gains more handling precision and discsOwned per level.
- You are required to create a custom leveling-up algorithm for each character type.

You are encouraged to create cutscenes or visual sequences (static images or videos) that play when significant milestones are reached, such as unlocking Kevin Flynn or defeating Clu. These narrative unlocks are intended to deepen immersion, rewarding both gameplay skill and commitment.

### 2.3 - Design Enemies (1 marks)

1. Design an Enemy superclass that represents AI-controlled opponents.
Each enemy should have attributes such as speed, handling, and aggressionLevel.
2. Design **5 unique enemies** that extend the `Enemy` class based on description in `enemies.txt`
3. Their positions on the arena are generated randomly each round.
4. Each time a new match begins, (seven) enemies (chosen from different types) are spawned.

// Define the Enemy class to represent in-game AI opponents.
class Enemy {
    String name;         // Enemy identifier
    String color;        // Jetwall color
    double speed;        // Movement speed
    double handling;     // Turning efficiency
    double aggression;   // Determines chase and attack logic
}


Character	Color	Speed	Handling	Description Playable
Clu	Gold	Very High	Aggressive	Corrupted intelligence, fast and strategic. No
Rinzler	Red	Very High	Sharp	Silent hunter — tactical and deadly. No
Sark	Yellow	Medium	Predictable	Enforcer AI, standard opponent. No
Koura	Green	Low	Erratic	Lowest-level AI, unpredictable but weak. No

Enemy AI behavior varies according to difficulty level. At lower levels, enemies move in predictable patterns. As difficulty increases, opponents may attempt to anticipate the player’s direction, flank from the sides, or recapture their own discs to reengage in combat.

Implement levels of AI difficulty:
- Koura → Easy → 10 XP - random but basic movement patterns.
- Sark → Medium → 100 XP - moderately intelligent, avoids walls, predicts player path.
- Rinzler → Hard → 500 XP - clever, makes strategic movies and collaborates.
- Clu → Impossible → 1000 XP - brilliant, unpredictable movement with logical but non-deterministic decisions.

Each bot must:
- Attempt to avoid collisions logically.
- React dynamically to player movement.
- Occasionally, make “human-like” mistakes for realism.




### 2.4 - Disc and Capture System (2.5 marks)

Discs are the core combat mechanic in Tron Light Cycles. Each player or enemy wields one identity disc.

1. Throwing and Recapture Mechanics
   - Players can throw their disc across a range of up to three grid units.
   - Once thrown, the disc stays where it lands until recaptured.
   - Players cannot throw another disc until one is retrieved.
   - A player may recapture their own discs or teammate discs of the same color.
2. Enemy Discs
   - Enemy bots can throw and recapture their own discs as well.
   - Enemies cannot pick up discs belonging to the player or other teams.
3. Effects
   - Being struck by a disc results in -1 life.
   - Colliding with a jetwall reduces 0.5 HP.
   - Falling off an open arena removes all lives instantly.
4. Skill Variations
   - As players level up, discs may travel faster or gain unique effects (e.g., ricochet, extended range).
   - Disc cooldown time may decrease with handling improvements.
5. You are not restricted to follow the following design. It only serves as a reference.

```md
Warrior
--> HP: [:::::           ] (45 / 60)
--> MP: [//////////////  ] (80 / 100)
+-------------------------------------------------------------+
OPERATION: 1 / 3

>> Starter
[S1] Attack
[S2] Defend
[S3] Heal                   < -20 MP, 0 / 3 CD, +200 HP, ->
[S5] Escape

>> spells
[A1] Roaring                < -10 MP, 2 / 3 CD,    0 HP, Cast silence>
[A2] <Locked - 10>
[A3] <Locked - 15>
+-------------------------------------------------------------+
```

### 2.5 Round-based Battle System (3 marks)

Now that we have characters, enemies, and discs in place, the next step is to implement the round-based arena system. In a text-based RPG game, players are allowed to engage in round-based battles through interfaces.

1. In each round, both players and AI-controlled enemies can make their moves, such as changing direction, throwing discs, or recapturing them.

2. The round continues until:
    - The player loses all lives,
    - All enemies are derezzed, or
    - The player chooses to exit the game.

3. Players can maneuver strategically, aim discs, or bait enemies into colliding with jetwalls.

4. The interface should clearly display the player’s HP, XP, number of active discs, and arena events.

> Tron deflects Rinzler’s disc!
> Sark collides with his own jetwall (-0.5 HP)!
> You recaptured your disc — energy restored!

5. Enemy AI should automatically respond to player movements. Depending on difficulty, they may choose to pursue, evade, or set traps with their jetwalls.

6. The arena system should provide concise but vivid feedback after each action, allowing players to easily understand the outcome of every turn.

```md
> You have HIT the skeleton warrior, causing 151 damage!

Skeleton Warrior
--> HP: [::              ] (27 / 60)
--> MP: [//////////////  ] (80 / 100)

> CRITICAL! Skeleton Warrior has SLASHED you for 57 damage!

Warrior
--> HP: [:::::           ] (45 / 60)
--> MP: [//////////////  ] (80 / 100)
+-------------------------------------------------------------+
>> Starter
[S1] Attack
[S2] Defend
[S3] Heal                   < -20 MP, 0 / 3 CD, +200 HP, ->
[S5] Escape

>> spells
[A1] Rabid Lunge            < -10 MP, 2 / 3 CD,    0 HP, Cast silence>
[A2] <Locked - 10>
[A3] <Locked - 15>
+-------------------------------------------------------------+
```

## 3 - Extra Feature Requirement (Total - 4 marks)

### 3.1 Save game functionality (1 mark)

It would be a great pity if someone couldn’t save their game progress or compare their achievements with others. Without these features, players would have to replay the same content repeatedly, and their accomplishments would not be recognized.

1. To enhance the player experience, implement a save system that records the player’s progress — including level, XP, and achievements — allowing them to continue from where they left off.
2. The game should prompt players to save before exiting, reminding them to preserve their current state.
3. Implement a leaderboard database (SQLite or MySQL) that stores:
    - Player name
    - Highest level achieved
    - Total score
    - Date of completion
4. Provide a Top 10 leaderboard accessible from the main menu to motivate players to improve their performance.

Consider using a database and the knowledge you have acquired in File I/O for implementing this functionality.

### 3.2 Story Progression and Visual Cutscenes (2 mark)

Mistakes aren’t the only thing that can interrupt a good game — lack of story flow can too. To create a truly engaging Tron experience, implement a story engine that reveals narrative sequences between gameplay stages.

1. The storyline should align with the Tron (1982/2010) universe — gradually revealing the history of the Grid, the rise of Clu, and Kevin Flynn’s legacy.
2. Players make choices that influence dialogue or unlock achievements and alternate story outcomes.
3. Cutscenes can be displayed as:
    - Text-based story transitions,
    - Static 2D art scenes, or
    - Embedded video clips (short and immersive).

4. Story content should be stored externally in a file (e.g., story.txt) to ensure modularity and easy updates.

This feature bridges gameplay and storytelling, offering players a reason to keep exploring the Grid beyond just survival.

### 3.3 Random Arena Generator (0.5 mark)

Repetition can make even the most polished game feel predictable. To keep each playthrough fresh, implement a random arena generator that dynamically creates new maps every time the game starts.

1. Each map must maintain logical playability — no unreachable areas or overlapping walls.
2. Include randomly placed ramps, barriers, and glow effects to add visual diversity.
3. Random seeds should vary for each game launch, ensuring no two arenas feel the same.

This encourages replayability and showcases procedural generation techniques suitable for grid-based games.


### 3.4 Aesthetic Enhancements and Achievements (0.5 mark)

Adding visual flair and a sense of accomplishment can greatly enhance player engagement.

1. Implement colored text and dynamic lighting effects to represent different factions and in-game states:
    - Blue for player actions
    - Red for enemy alerts
    - Gold for bosses or achievements
2. Include ASCII visuals or glowing UI panels for menus and battle interfaces to reflect Tron’s neon aesthetic.
3. Introduce achievement notifications, such as:
    - “🏆 Survived 3 Rounds Against Clu!”
    - “✨ Defeated Rinzler Without Losing a Life!”
4. Store UI elements, ASCII art, and achievements in dedicated resource files (e.g., ui.txt, achievements.txt).

Feel free to incorporate any other features that you find interesting! Don't confine yourselves to the assignment question. Get as creative as you can, because there are no limits!


## 4 - Reminders

### 4.1 Modularity

#### 4.1.1 Object-Oriented Programming (OOP)

You need to apply the principles of Object-Oriented Programming (OOP) in your code to eliminate redundant code. It is important to grasp the concept of abstraction and effectively utilize classes, abstract classes, interfaces, and enums. Let's consider the following code as an example:

```java
class Monster {
    int healthPoints;
    int mana;
    List<String> status;    
}

class Hero {
    int healthPoints;
    int mana;
    List<String> status;
}
```

Instead of duplicating the variables `healthPoints`, `mana`, and `status`, we can create a suitable parent class to achieve abstraction. For instance:

```java
class Character {
    int healthPoints;
    int mana;
    List<String> status;
}

class Monster extends Character {

}

class Hero extends Character {

}
```

By refactoring the code in this manner, we indeed improve scalability and maintainability.

#### 4.1.2 Single Responsibility Principle (SRP)

<div style="text-align:center">
    <img src="image/srp.png" alt="Single Responsibility Principle" width="400" height="250">
</div>

The Single Responsibility Principle is a fundamental programming principle that states that *A class should have only one reason to change.* It emphasizes that each class should be responsible for a single behavior or functionality.

In the given example, while applying OOP, it is important to ensure that each class is responsible for its own specific behavior. For instance, a `PlayerCycle` class may be responsible for attacking monsters or healing teammates, but it should not handle tasks unrelated to its core purpose, such as interacting with the operating system or managing database connections. Applying the SRP helps in maintaining cohesive and focused classes.

### 4.2 Using Git and Github for Cooperation

#### 4.2.1 Stop using Whatsapp or Telegram for exchanging .zip file!

It's quite common for newcomers who have no prior experience in programming to collaborate with others by sharing .zip files or sending .java files. However, this approach can lead to several issues.

1. The recipient needs to review all the code to identify the changes made, which can be time-consuming and error-prone.

2. If the recipient accepts all the changes and a bug is later discovered, it becomes challenging to revert to a bug-free version.

3. Frequent code changes can create confusion, especially when files are shared with different names or under the same name.

Therefore, it's advisable to refrain from using platforms like WhatsApp or Telegram for exchanging .zip files. Instead, consider using version control systems like Git and platforms like GitHub or Bitbucket, which are designed for efficient and collaborative code management.

<div style="text-align:center">
    <img src="image/git-and-github.png" alt="Image Description" width="400" height="220">
</div>

Among the various version control systems (VCS) available, Git stands out as one of the best options. Although some people may mistakenly believe that Git and GitHub are synonymous, they are, in fact, distinct entities.

Git is a distributed version control system designed to track changes in computer files. It excels at facilitating collaborative software development among programmers. Its key objectives include speed, data integrity, and support for distributed and non-linear workflows.

On the other hand, GitHub serves as an online hosting service specifically tailored for software development and version control using Git. It enhances Git's capspells by providing features such as access control, bug tracking, software feature requests, task management, continuous integration, and project wikis.

In your assignment, it is crucial for you and your teammates to leverage Git and GitHub for effective team cooperation. Merely relying on copying and pasting or sharing ZIP files might suffice for small projects. However, as the codebase grows significantly, such approaches can lead to disastrous consequences. Utilizing Git and GitHub ensures streamlined collaboration and mitigates the challenges associated with managing large-scale projects.

#### 4.2.2 Recommended resources on studying Git

You might refer to the [Missing Semester | Lecture 6 | Version Control (Git) (2020)](https://www.youtube.com/watch?v=2sjqTHE0zok) and [GitHub Basics Tutorial - How to Use GitHub](https://www.youtube.com/watch?v=x0EYpi38Yp4) for more details.

#### 4.2.3 Brief Guideline on Using Git

```bash
# Configure your Git with a username and email
git config --global user.name "Your Name"
git config --global user.email "youremail@yourdomain.com"
```

If you've recently downloaded [Git](https://git-scm.com/), it's essential to set up your username and email. This information helps identify who made specific changes. If you have any inquiries about the changes, you can easily reach out to the contributor via email.

```bash
# Clone your repository from GitHub
cd path/to/your/code
git clone <GitHub_Repository_URL>
```

Once your Git configuration is in place, the next step is to register an account on GitHub and create a new repository. Copy the GitHub repository URL and paste it into the code snippet as indicated.

```bash
# Share your changes with your team
git add .
git commit -m "✨ Added new features"
git push
```

After making changes, like creating a new function such as `Login`, and wanting to share your work with your team, you should push the changes to the remote repository so that others can benefit from your code. Here's a breakdown of the commands:

- `git add .` stages all changes for commit.
- `git commit -m "your message"` provides a commit message to describe your changes.
- `git push` indicates that you've finalized your changes, at least in their current state, and you're ready to share them with others.

#### 4.2.4 Writing a good commit message

Writing informative commit messages and committing changes frequently not only helps others understand the modifications you've made but also enables easier access to specific older versions. A well-crafted commit message can serve as a helpful update log. Let's compare the following examples:

```bash
git commit -m "Add new files"
git commit -m "New updates"
git commit -m "Some changes"
```

and these messages:

```bash
git commit -m "Implement login authentication"
git commit -m "Fix bug in loading the file"
git commit -m "Implement embedded database for storage"
```

Which set of messages is more descriptive? Undoubtedly, the second set is more informative.

It is important to understand that commit messages should accurately reflect the changes made in the commit. The messages should be concise yet descriptive, providing a clear understanding of the modifications introduced. By following good commit message practices, developers can enhance collaboration and make it easier for others to navigate and utilize previous versions of the codebase.

### 4.3 Writing readable code

<div style="text-align:center">
    <img src="image/programmer-meme.png" alt="Image Description" width="300" height="300">
</div>

Code is read more often than it is written. Avoid trying to be overly clever. While it may seem impressive to code swiftly with three-character variables or craft complex one-liners with numerous loops and clauses, both your present and future selves, along with your teammates, will benefit from the improved readability that comes from taking the time to give your methods and variables meaningful names, maintain proper spacing, and add meaningful comments. Always approach coding as if you'll need to explain it a week later, because the reality is, you will, even if it's just to yourself.

There are generally three naming conventions, which are known as camelCase, snake_case and PascalCase. You might refer to [This Article](https://www.freecodecamp.org/news/snake-case-vs-camel-case-vs-pascal-case-vs-kebab-case-whats-the-difference/#snake-case) which clearly explains everything you would need for the naming convention.

## 5 - Contact Me

For any questions or clarifications, please contact me, Mohammad Shahid Akhtar, via WhatsApp or Telegram at 014-8784386, or by email at 22052133@siswa.um.edu.my. However, WhatsApp and Telegram will always be the preferred choices. If you contact me through email and I don't reply within 24 hours, please feel free to contact me through those messaging apps.

If you are seeking for the possible input and output, you might watch the following videos on Youtube:

1. Snake Game in Java – Java2D Package Tutorial
2. Artificial Intelligence Pathfinding for Grid-Based Games
3. SQLite Database Integration in Java Applications
4. Version Control with Git and GitHub
5. The Making of Tron (1982) – Film Reference

