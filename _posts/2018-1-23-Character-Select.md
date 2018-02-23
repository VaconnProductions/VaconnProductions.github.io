---
layout: post
title: Character Select Part 1
---

While the characters are being animated, the character select was worked on (mostly in class), and it's been coming together. Players can swipe through characters, pick them from the grid and switch between battalions very easily. 

![SelectScreen](/images/SelectScreen.gif "SelectScreen")

The gif just shows: switching characters, picking characters and switching battalion. 

## Code

In terms of code there is nothing crazy going on, a lot of Unity specific code was learned while making this menu which should hopefully help with the rest of the game. I'll just point out a few cool things that came up while writing this and maybe it can give a heads up to others. 

# Sort
When sorting the characters in the grid, enumerations made sorting dead simple. In a nutshell, it creates a set of values that belongs to an "enumeration" class and each value is assigned to an integer starting from zero. 

{% highlight C# %}
public enum Empire { Roman, Greek, Persian, Chinese, Japanese, British, Egyption}
Empire value = Empire.Persian; 
// (int)value = 2 , "Persian" has an index of 2 in the enum
{% endhighlight %}

So when it came to sorting it was as simple as
{% highlight C# %}
GameObject[,] CharEmpires  = new GameObject[10,10]; 
for (int i = 0; i < availableCharacters.Count; i++)
{
    CharEmpires[(int)availableCharacters[i].Allegiance,(int)availableCharacters[i].CharacterClass] = Instantiate(baseIcon);
}
{% endhighlight %}

# Enumerator
A Unity function which I've already abused is Coroutines. They allow you to run a function, specifically of return type IEnumerator, and wait for the following update frame or time to continue at any point within the function. 
For instance: 

{% highlight C# %}
private IEnumerator ClearName()
    {
        while(CharacterName.text.Length > 0)
        {
            CharacterName.text = CharacterName.text.Remove(CharacterName.text.Length - 1);
            yield return new WaitForSecondsRealtime(0.05f); 
        }
    }
{% endhighlight %}
Here is a simple function which clears the players name in the menu. when the compiler reaches "yield return" the function is left and comes back after the specified time/frames, in this case 0.05 seconds. Very usefull stuff and a must learn when starting Unity in my opinion. 

I'd love to show something technical but Unity does everything for you, which goes to show anyone can really make a game. I do recommend trying it out if you have the desire to! Anyways take care for now!

-Kashif
