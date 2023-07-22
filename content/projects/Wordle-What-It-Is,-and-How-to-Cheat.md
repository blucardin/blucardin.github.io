---
title: "Wordle: What It Is, and How to Cheat"
date: 2023-07-22T02:03:27-07:00
draft: false
---


I wrote an article for my school newspaper (The Franklin) that details my efforts to find the best wordle starting words using code-based analysis with probability and statistics.


# Wordle: What It Is, and How to Cheat 

Word games are not old, but there is a new one that has been taking the internet by storm: WORDLE! A web-based interactive game made by Josh Wardle that was recently bought by the New York Times for seven-figures. You can play the game here: https://www.powerlanguage.co.uk/wordle/. 

The rules are simple, guess a 5-letter word in 6 tries. For every letter in each try, the game will tell you if it is not in the word, in the word but in the wrong place, or in the word and in the right place. 

<img style="float: right; margin: 20px;" src="/images/squid-wordle.png"/>


Playing wordle is very fun, especially the sharing aspect of the game. It is easy enough that anyone can play, but hard enough that only top linguists can win. This makes a system in which people see their friends bragging about getting a wordle online, then trying it for themselves, eventually winning, and sharing it. In a sense, wordle has become a polarizing infection of the internet, with people either loving, or hating the game. 

But why play when you can cheat? None of your friends will ever know and being able to solve any wordle at any time makes the game more fun. Due to its complexity, (there are more than 17000 5-letter words, and you need to guess it in only 6 tries) it is difficult to cheat the game. However, with a lot of brute force, it gets easier. 


Before one can learn to cheat wordle, they must understand it. To guess the correct word, not only involves luck, but decision making. Each guess that is not the correct one, gives you at least information about what letters are not in the word, and at most tells you which letters are in the word, and their places. From this, one technique for brute forcing the game becomes apparent: choose three words with completely different letters, then from the information you get, come up with the final word. 

For example, one might use the words: 

Panic
Doubt
Shrew

But we can get even better. If we use the most used letters to construct these words, each word will give us better information, because if the letter is not in the word, it eliminates the most possible words that can be the wordle. If we use the most probable letters, (found here: https://www.sttmedia.com/characterfrequency-english) we get: 

Tenia
Chord
Fugly

With a little more work, we can have even better words. Instead of using the most probable letters in the entire English language, we can focus on the letters that are most probable in 5 letter words. However, there is no place on the internet that clearly states this, so we must do some digging ourselves. 

By downloading The Online Plain Text English Dictionary (found here: https://www.mso.anu.edu.au/~ralph/OPTED/) and parsing it using a python script, we can create a .csv file with most of the words in the English dictionary, 176,048 to be exact. According to Oxford dictionary, only 171,476 out of 600,000 words are in current use today, so we are close enough. This csv file can be easily read and processed by other python programs. If we sort that csv for only 5-letter words, then count the occurrence of each letter and calculate their probability we get the following percentages: 



e
11.26%,
a
8.76%,
r
7.95%,
s
6.89%,
t
6.54%,
o
6.28%,
l
6.26%,
i
5.61%,
n
4.57%,
c
4.36%,
u
3.81%,
h
3.67%,
d
3.44%,
p
3.14%,
g
2.51%,
y
2.43%,
m
2.43%,
b
2.27%,
f
1.88%,
k
1.82%,
w
1.73%,
v
1.28%,
z
0.31%,
x
0.30%,
q
0.27%,
j
0.21%



Using these updated percentages, we get the words:

Rates
colin
Pudgy
(and if you really need one more) whomp

Now, this seems like the end of the story. How can one guess the wordle better? By cheating even more! Using a scrabble word finder with advanced features, (found here https://scrabblecheat.com/scrabble-cheat-center.aspx) anyone with enough means can easily find the correct word. All you need to do is search for words with 5 letters using the letters you have, then filter the results for the letters you don’t have. If you want more control over your searches, you could try using a regex searchable dictionary, https://visca.com/regexdict/.


As you can see, in these instances, all uses of rates, colin, etc. resulted in immediate yellows. 

<!-- insert the images in the imgae folder wordle1, wordle2, wordle3, so they are side by side -->
<!-- on scaling, resizee the images -->
<style>
    .image-container {
        display: flex;
        justify-content: space-between;
    }

    .image-container img {
        max-width: 100%;
        height: auto;
    }
</style>

<div class="image-container">
    <img src="/images/wordle1.png" alt="wordle1" width="30%"/>
    <img src="/images/wordle2.png" alt="wordle2" width="30%"/>
    <img src="/images/wordle3.png" alt="wordle3" width="30%"/>
</div>

With great power comes great responsibility. Now that you know the ways of the wordle, make sure to constantly post your wins on social media and pass them off as real.  

All code used for this demonstration can be found at https://github.com/blucardin/wordle 

https://nypost.com/2022/01/31/new-york-times-buys-wordle-from-josh-wardle-for-seven-figures/   

https://www.mso.anu.edu.au/~ralph/OPTED/ 

https://drive.google.com/file/d/14iy26TW7uewiZqkiOKoW2BP8OwYOcFaq/view 

https://englishlive.ef.com/blog/language-lab/many-words-english-language/ 

https://www.sttmedia.com/characterfrequency-english 

https://scrabblecheat.com/scrabble-cheat-center.aspx

https://twitter.com/cairn4/status/1488894756906274823 

https://www.powerlanguage.co.uk/wordle/  
