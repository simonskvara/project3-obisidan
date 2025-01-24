## Week 1 (3.12. >)
This week was a 'cooldown' week. We worked a lot for the Vertical Slice deadline and wanted to rest a little bit and work on the other classes. Everyone in the team agreed to this so there wasn't much work done during this week.

## Week 2 (10.12. >)
I have discovered a major flaw in my ability system. Whenever I put a mark on multiple enemies at the same time the marks interfere with each other, making it so that it will not give damage as it is supposed to each enemy that has a mark, but it only gives damage to one enemy at a time even if there is multiple enemies marked. And that is because the ability is made through a Scriptable Object. I don't know I could have been so stupid, when it is so obvious. There is only a single instance of it and it is not initialized like a normal script would be, and therefore when I am referencing something or decreasing/increasing a timer all off the mark interfere with this one instance. 

So while I have been able to so far make it flexible and readable, to fix this quickly I unfortunately made it more confusing. To be clear, I only had to change how the mark works the other abilities I didn't have to touch. However, I had to change the EnemyMarkHandler. I had to make it a per-enemy basis. Basically the handler script has a dictionary in it and whenever I mark an enemy it will log the enemy and a struct MarkState that has all the information for the mark and add it into the dictionary.
In the ability scripts themselves, I then get a reference to the dictionary and manipulate the values in there.
It is incredibly confusing but it works. I am very upset I didn't realize this problem sooner, because I would have done it a different way. The one upside to this is that at least, it is easy for game designers to balance the abilities, since they are nicely done in a scriptable object and they just add those to ability pools however they want. I am incredibly upset though, how it turned out in the backend.

Also there was a nasty Git problem where a bunch of work somehow got deleted in a merge, thankfully Benny helped us to resolve the problem.

## Week 3 (17.12. > + Holidays)
During this period I didn't do much except making some abilities and fixing bugs.
We however had the playtesting evening and we had some feedback. Mostly it was lot of quality of life and small things that they would like to have in the game to feel better. Obviously it is an action game and we need it to feel better. We were still lacking in visual communication however it was much better now that we also had a light up for when the enemy is damaged. I also used the same effect for when the player heals. They also had a lot of balancing 'complaints' that we did take to heart to make it feel better. It is genuinely insane how much the playtesting evening can help, since whenever I am testing out something myself I get used to it and don't see all these small mistakes.

There was a suggestion to put the mark that is attached to enemies somewhere else than the center of the enemy, so that it is visible who is marked. That is a good idea that even Clara brought up before, however I don't think we implemented that, I don't know why. Perhaps it was lack of time? Or it was that we forgot since we had so much to do.
What is also such a conundrum is keybinds. Every time there is a playtesting evening, there is always someone who doesn't like the keybinds. Even Mike would like it differently. The problem with that is that everyone has different preferences. We could empirically analyse the best control scheme and have that as default but everyone has small preferences. All that could be solved by adding rebinding. However, we have little time and a lot of stuff to do so I couldn't do it. We will just recommend to play with controller.

I planned on working on some small stuff during the holidays, however that fell through since I tasted the feel of relaxing and I didn't want to stress myself with the project.

## Week 4 (7.1. > )
This is the week right after holidays where we realized that we only have a week left until the deadline and not 2 weeks. We realized we might be screwed. Luckily we managed to extend the deadline by 3 days. 

During this week I finished the abilities I have yet to do. However mostly I wasn't creating 'content' for the game anymore. My occupation was to add the 'game feel', like sounds and screen shakes. 
So for that I made a simple audio system using the Audio Mixer in Unity. It is not perfect since the volume is controlled through decibels and they function exponentially, meaning that sliding the volume bar halfway basically mutes the sounds. However that is enough for the time we had. I figured out how to make spatial audio for a 2d game and it is surprisingly easy. Normally audio listeners are on the camera and that would be bad since spatial audio is for 3D and the camera is away from the plane. So I just put the audio listener on the player. Since I wasn't doing anything content wise I was sourcing sound effects. Who knew it could be so hard to find sound effects for the stuff we need. I downloaded so many free sound packs off of Itch. Luckily I found acceptable ones and now it feels very nice having some sound feedback to the player actions. The hardest one to figure out was the mark sounds. You want a sound effect that is prominent enough that you can hear it during combat, but you don't want it to be so annoying that it distracts the player. I think I however found some that are fine enough. For anything more we would need a sound designer. 

Also at the end of this week we had the playtesting between classes with the Build a Toy class. Thanks to the new input system we had the game interactable with a controller. We found out that the game feels so much better with a controller. Why? Well the bigger control over direction I think is the main one. On a keyboard you only have 8 directions you can go in, but a controller adds much more to not only direction but movement as well. Next step is to figure out how to make the UI interactable with a controller too.

## Final Stretch
The final stretch is the 3/4 final days that we got by extending the deadline. In here I mainly focused on the stuff that we needed to have like the Seed functionality or controller UI support and just generally tying everything together. 

I initially thought that the seed functionality would be much harder to do, but there is a Unity Random method called InitState that does that for me. I just need to call it before any Random stuff happens and they will take that seed. I basically just then store the seed in a scriptable object, from the input field in the main menu and then in the main scene if the seed is 0 i generate a random seed and if it is not 0 i use that value. Also found out it doesn't have to be just positive but a negative Int32 can be a seed too.

Next thing is making the UI interactable with controller. So while unity basically has the function for that already, there are a couple of caveats. I can add the first selected to the event system, but what happens when I change the menus, or open a different menu on top and then close it, now the selected button won't even be there. So I had to add to scripts to change the selected object anytime something like that happened. 
However there is something that just grinds my gears. The Input field. While it is a Selectable when you go into it with a controller you are unable to leave and are forced to use Escape on keyboard. No button on the controller worked to leave the input field. So I had to make my own script, where it is possible to leave the the input field when I do something to change the selectable. That worked but here comes the infuriating part. 
![[Pasted image 20250120163121.png]]
This would happen. Instead of going to the Toggle it would go to the button down there no matter what I would do. I even explicitly told the Selectable to go next to the Toggle I even explicitly referenced the Toggle in the script, yet for some reason it always went to the Back button. This bewildered me so much. I could come up with no reason what could make this. I eventually gave up because I spent too much time on it already and there was stuff to do. 

Once I was done with this I helped with the Cerberus boss fight. Due to constraints we couldn't make it pretty but it was nice. There were supposed to be animations I was to implement but there was literally no time so there are only some simple looping animations. I also had to lock in at the end and bring everything together because the deadline was approaching and we had to have a win condition. Thanks to Clara we have a very nice UI and Thanks for Playing scene. We managed to upload the build 5 minutes before deadline. 

And then we celebrated 🎉
We finished the game and we were quite proud of it as well.

Much to our disappointment, somewhere along the final touches some UI unreferenced and because of that the abilities weren't displayed and the ability selection wasn't closing. 
It is very sad that a bug like this got through like this.
We all hope that Jorg got to play the version with this fixed. 

But despite this hiccup we were proud to finish it.