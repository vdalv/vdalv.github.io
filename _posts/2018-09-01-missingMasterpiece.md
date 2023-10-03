---
layout: post
comments: false
title:  "The Case of the Missing Masterpiece"
date:   2018-09-01 00:01:02
---

Project completed: Feb. 2020, Post published: Oct. 2023

### Introduction

One summer a few years ago, I stumbled onto Theadless.com, where I decided to rate a few t-shirt designs. At one point, I came upon a design that I found completely hilarious. According to my memory, it was a drawing of a bearded man riding a bike, with a solid, mustard-yellow background and colorful confetti in the air. I attempted to find that design by querying the Threadless archives, but had no luck. I looked into writing a Python script to loop through all 150,000+ designs from the general timeframe (2012 – 2015) that I originally witnessed it, and picking out all the predominantely-yellow images. The recommended solutions I found from a quick online search seemed extremely inefficient, and I couldn’t find any pre-built solutions that met my needs, so I decided that this was a practical excuse for me to embark on my first image classification problem.


### Data Collection
I began the project by taking the first 2,003 images (not sure why I grabbed the three additional images at this point) from the original 150,000+ image dataset, and picking out the very (mustard) yellow ones. This yielded 45 “yellow” images, and 1,958 “not yellow” images (see Figure 1).

### Training Overview
After some brief research into existing image classification tools, I decided to use darknet's image classifier (fine-tuning the Densenet 201 model). My process was:
1. Train/fine-tune the classifier for a few hundred epochs
2. Select a checkpoint with a relatively low loss
3. Use the fine-tuned model to classify all the remaining design images
4. Review all the images that the model was 70+% sure fell into the 'yellow' class, sorting out the false positives, and all the while look for the masterpiece
5. Add the sorted result images ('yellow' and 'not yellow' classes) to the 'train' and 'val' folders

My initial results were pretty good, so I ended up repeating this process multiple times (seven total runs). I've included images of the training and result images below. Note: After take 3, I lowered the threshold to 50%, as the number of 70+% confidence images had become very low. Also, instead of relying on one just checkpoint, I ran various different checkpoints (i.e. 150 - 300, separated by 50 epochs) against the remaining design images.

### Training - Take 1
[![](https://i.imgur.com/KRo8dOq.jpg)](https://i.imgur.com/LX63jyY.jpg)
(Figure 1. The initial 2,003 images used in the first training set. Note: 'train' folder on the left, 'val' on the right)

The results:
[![](https://i.imgur.com/NoTLPYL.jpg)](https://i.imgur.com/Lwiu1B0.jpg)
(Figure 2. Images that the model detected as yellow with over 70% certainty, after I've manually gone and sorted them into what I believe are the proper classes ('yellow' on the left, and 'not yellow' on the right). Overall results: 81 'yellow' images, 8 'not yellow' images = 89 Total)

### Training - Take 2
[![](https://i.imgur.com/Gro1vhU.jpg)](https://i.imgur.com/8CF8LHo.jpg)
(Figure 4. Take 2 training data)

[![](https://i.imgur.com/oVqoPuC.jpg)](https://i.imgur.com/YG2kRJj.jpg)
(Figure 5. Take 2 results: 34 'yellow' images, 12 'not yellow' images = 46 Total)

### Training - Take 3:
[![](https://i.imgur.com/SByCF1U.jpg)](https://i.imgur.com/1D9QcHG.jpg)
(Figure 6. Take 3 training data)

[![](https://i.imgur.com/6DtHkZk.jpg)](https://i.imgur.com/FwdUijA.jpg)
(Figure 7. Take 3 results: 754 'yellow' images, 454 'not yellow' images = 1208 Total)

### Training - Take 4:
[![](https://i.imgur.com/SoED9kV.jpg)](https://i.imgur.com/5JecDJB.jpg)
(Figure 8. Take 4 training data)

[![](https://i.imgur.com/v4tMrxP.jpg)](https://i.imgur.com/ZEpreO1.jpg)
(Figure 9. Take 4 results: 117 'yellow' images, 343 'not yellow' images = 460 Total)

### Training - Take 5
[![](https://i.imgur.com/FWpkmOv.jpg)](https://i.imgur.com/cz1OnrJ.jpg)
(Figure 10. Take 5 training data)

[![](https://i.imgur.com/U22QQYs.jpg)](https://i.imgur.com/Sh1ICiL.jpg)
(Figure 11. Take 5 results: 177 'yellow' images, 1568 'not yellow' images = 1745 Total)

### Training - Take 6
[![](https://i.imgur.com/jMkdqll.png)](https://i.imgur.com/L89MQ71.jpg)
(Figure 12. Take 6 training data)

[![](https://i.imgur.com/XoEIKAs.jpg)](https://i.imgur.com/JGYWRrU.jpg)
(Figure 13. Take 6 results: 819 'yellow' images, 1807 'not yellow' images = 2626 Total)

### Training - Take 7
[![](https://i.imgur.com/PGJ4f75.png)](https://i.imgur.com/Wti3rMT.jpg)
(Figure 14. Take 7 training data)

[![](https://i.imgur.com/nJ1qEL5.jpg)](https://i.imgur.com/KeEl4eO.jpg)
(Figure 15. Take 7 results: 165 'yellow' images, 82 'not yellow' images = 247 Total)

---

At this point, after seven unsuccessful attempts at finding the masterpiece, I decided to put this project on a bit of a hiatus and work on some other interesting projects (mainly GANs). I was beginning to wonder if the masterpiece was one of the 461 broken images that I'd discovered in the dataset (images that had uploaded improperly, or been removed from the Threadless archive by their creators)...

### PyTorch Training
After hearing much about PyTorch, I decided to finally take it for a spin by applying it to my lingering image classification project. I found some documentation, and was soon on my way. I started completing steps 4 and 5 of my above process, in order to create a new dataset for this latest attempt (#8). However, out of a bit of laziness and impatience, I decided to just take the 'Take 7' training data and throw it, wholesale, into PyTorch.

From the beginning, the training statistics were impressive — I was getting 90+% accuracy as early as the 2nd epoch. I stopped the training process when I noticed that the training stats had plateaued, and ran the checkpoint with the most impressive train and validation stats against the remaining Threadless design dataset (135,000+ images).

### Results - Take 8
Training data = same as 'Take 7' in Figure 14.

![](https://i.imgur.com/p75vic1.jpg)
(Figure 16. Take 8 results: 3,223 Total)

I scrolled through the results folder reviewing the images, and began to get nervous around the 50% mark. However, I spotted it at last:
\
\
\
\
\
\
\
\
\
\
\
\
\
![](https://i.imgur.com/MaoTzO2.jpg)
(Figure 17. The masterpiece. This design was simply titled 'ridin-2', but unfortunately I'm unable to find it on the official Threadless archives now, to give credit where credit is due.)

### Conclusion

Overall, this was an interesting and entertaining project, with a couple lessons learned.
1. __Don't hesistate to try out other models/frameworks/approaches__. 
2. Data is critical, and continues to take a lot of time to deal with, as a few experts have also concluded:

![](https://i.imgur.com/WvWcmI4.png)
(Figure 18. Unknown source)

![](https://i.imgur.com/h3vaEzz.png)
(Figure 19. Andrej Karpathy Twitter post I believe.)

![](https://i.imgur.com/s05viV5.png)
(Figure 20. Twitter discussion)

![](https://i.imgur.com/9J8NyWE.png)
(Figure 21. Twitter discussion)
\
\
\
\
Thanks for reading, and God bless!
