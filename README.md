# GAME PROGRAMMING - EX - 6

## EXP - 6 AI Random Roam with Chase - Unreal Engine

## Name : kirthick rosahn j
## Reg no : 212223040097

##  Aim
To create an AI character in Unreal Engine that roams randomly within a NavMesh area and chases the player when they come within a certain range, using Behavior Trees, Blackboard, and AI Perception.

##  Procedure

1. **Setup Navigation**
   - Add a `NavMeshBoundsVolume` to your level and scale it to cover the roamable area.
   - Press **P** to confirm the green nav area is visible (indicating navigable space).

2. **Create AI Character**
   - Create a Blueprint character (e.g., `BP_AIEnemy`) with a skeletal mesh and AIController class.
   - Create an AI Controller Blueprint (e.g., `BP_AIController`) and assign it to the character.

3. **Enable AI Perception**
   - In `BP_AIController`, add an `AIPerception` component.
   - Configure a **Sight** sense (set detection range, lose sight range, peripheral vision angle).
   - Bind `OnPerceptionUpdated` to update a blackboard value (e.g., `CanSeePlayer` and `PlayerActor`).

4. **Set Up Blackboard**
   - Create a Blackboard with the following keys:
     - `TargetLocation` (Vector)
     - `PlayerActor` (Object)
     - `CanSeePlayer` (Bool)

5. **Create Behavior Tree (BT_AI)**
   - Structure it like this:

     ```
     Root
     └── Selector
         ├── Sequence (Chase Player)
         │   ├── Blackboard Check: CanSeePlayer == true
         │   └── Move To: PlayerActor
         └── Sequence (Random Roam)
             ├── Task: Find Random Location → TargetLocation
             └── Move To: TargetLocation
     ```

6. **Custom Task: Find Random Location**
   - Create a new `BTTask_BlueprintBase` to get a random reachable point using:
     ```cpp
     UNavigationSystemV1::GetRandomReachablePointInRadius()
     ```
   - Set the result to the `TargetLocation` blackboard key.

7. **Test the AI**
   - Add a player character to the level.
   - Place the AI enemy in the map and assign its controller and behavior tree.
   - Press **Play**: the AI should roam when the player is far and chase the player when within sight.
  

## Output

<img width="1919" height="1023" alt="op1" src="https://github.com/user-attachments/assets/c9d0721a-b486-4c25-8907-774501096217" />

<img width="1919" height="1017" alt="op2" src="https://github.com/user-attachments/assets/9766449c-1f2b-411a-818d-39aa2f74e96c" />

<img width="1016" height="428" alt="op3" src="https://github.com/user-attachments/assets/6c3201ca-08fc-4990-87ec-478f4fe0111a" />

<img width="1297" height="498" alt="op4" src="https://github.com/user-attachments/assets/7ebd4b62-4a0e-44bd-bc76-a72b2697d942" />

## Result
The AI character roams randomly within a defined area. When the player enters its sight range, the AI stops roaming and begins to chase the player until the player is out of sight, after which it resumes roaming.
