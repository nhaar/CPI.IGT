# Club Penguin Island IGT & Load Remover

This repository contains the code for a Club Penguin Island mod which adds an in-game timer with load remover, meant for speedrunning.

# Installing

Download the dlls provided in the releases tab, place them in your game's Client\ClubPenguinIsland_Data\Managed folder.

# Features

The in-game timer is displayed on the screen. You can change the timer settings by opening the game's offline mode menu, which explains in detail what each settings does. The timer uses in-game time (frame count), except for when you close the game in which it will calculate the time spent with the game closed (real time), the final result will be a mix of the game time (which means lag will not influence the time in-game) and real time.

# Limitations

* Changing the computer time when the game isn't open will break the timer. Changing it while the game is open is fine.

* The load remover only works in one instance of the game at a time. Make sure you are on the correct instance when you have to open more than one game. More details can be found in the timer settings menu in-game.

* Because of Unity's time functions, the accuracy of the real time can't be of more than 1 ms, which means that in a run where you open and close the timer multiple times, the accuracy might be off by 10-20 ms (around 1 frame at 60 fps).

* If you manage to somehow close the game and swap to a new instance in less than 150 ms, you could technically lose time because the load remover won't be working yet. It shouldn't be possible for a human to swap the instances that quickly, but it's important to keep that in mind for TASing.

* The timer will not work properly if you alter the IGT_Data folder, and the timer may either stop working or display innacurate times.

# Editing The Game (Only for people who want to contribute to this mod)

The code in this repository contains C# code meant to be injected into the decompiled game code. I recommend using [dnSpy](https://github.com/dnSpy/dnSpy) to decompile and edit the code.

To inject the code properly, first change the LoadingController class in the Disney.Kelowna.Common namespace in UnityShared.dll just like in  `loadingcontroller.cs `. Then, change the main script, which should be one that runs every frame and is initialized at the beginning, according to  `main.cs `. I've picked ZoneTransitionService from the ClubPenguin class in ReMix-Game.dll, if that is to be changed the other code will need to be changed too. The other two things to change is the QuestService class, in the ClubPenguin.Adventure namespace and the GameSettings class in the ClubPenguin namespace, both in the ReMix-Game.dll, which you can copy the code in  `questservice.cs ` and  `gamesettings.cs `. If using dnSpy and you get a compile error, make sure you are editing a method and not the class, and if you are still getting a weird decompile issue close the dll you are editing and open it again as that (this always happens to me a few times in the same few scrips).