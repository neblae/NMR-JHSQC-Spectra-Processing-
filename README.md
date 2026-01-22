# NMR-JHSQC-Spectra-Processing-
Creating a script that inputs NMR FID signals from JHSQC protocols and outputs all metabolites integrated by area in order to determine metabolic flux

Background information:
NMR (Nuclear Magnetic Resonance) is a analytical technique characterized by its use of magnetic fields and radio waves to manipulate atomic nuclei. It collections information on a molecule
by shooting strong magnetic fields through a sample, aligning all nuclei in a molecule with the magnetic field. When released, the nuclei move back to its original position, and that movement (known as the relaxation period) is what is measured by the instrument. In return, you are given what an FID (free induction decay), and this will be the input for the script. 
  There are multiple types of NMR: the most common being 1H NMR, meaning that the relaxation of Hydrogen atom nuclei is being measured and turned into an FID. For this experiment (JHSQC) we are using 13C NMR. Reason being, 13C is a rare isotope of carbon (the normal carbon being 12C) and it is important as 13C is radioactive. Since our experiment is designed to examine how carbon metabolites (the molecules that turn into energy in your body, namely sugars), 13C is very useful as it can be used to mark specific carbons that get broken down into other derivatives. 
  <img width="1122" height="709" alt="image" src="https://github.com/user-attachments/assets/dee2b23f-d701-423e-a789-01a845dba559" />
  This is an example of an FID from one of my own experiments. It is what is turned into a normal spectra with peaks, which can be read and deciphered to determine what metabolite is present at that given moment. It also gives insight into how much of the metabolite is present in the sample. 
<img width="1116" height="739" alt="image" src="https://github.com/user-attachments/assets/59f0a8c8-9662-4f58-9cf5-a78732cf5c9f" />
  (this is what is looks like post processing)

The challenge for writing the script is mostly in being able to replicate the signal processing that is usually done automatically by TopSpin, the NMR processing software. I'm sure there is documentation on how much of the processing is done, but what is difficult is how our protocol is very specifically tailored for our type of experiment. Here's why:

As mentioned earlier, the goal for using NMR in our experimentation is to track how metabolites change over time. This is already a more advanced application of NMR; since you are all probably math majors reading this, it's like having an exponential function, and then taking the derivative of the function to determine the rate of change (or something like that since I'm not a math major). We are taking multiple shots of the sample over time in order, and in return we are given hundreds of NMR spectra where you can see different parts of the graph (correlating to different molecules) slowly increasing and decreasing over time). This is not what we need to replicate in code, but what we do need to replicate is how we changed the 
protcol for the NMR, and thats because we are doing JHSQC NMR, or J-Coupled Heteronuclear Single Quantum Coherence. What that means exactly, we probably don't need to know exactly, since it is related to HOW the data was collected; but in case it is important, I believe the data had to be quantum coupled before recording the FID. 

That's just the background and what NMR is gonna be used for. There's a lot of signal processing in this, and I believe nmrglue lib works well to provide functions that do most of what TopSpin does. 


Script will aim to NMR spectra into metabolitic markers in a stepwise process:

1. Inputs FID and processes it into a readable 2D spectra
     - what we want to replicate in the script are the commands that I usually imput in the software. First I apply window functions, changing them to EM and Sine. Then I apply xfb, which is the fourier transform. Then I apply abs1 and abs2, which is the phase correction. [The confusing part is if there are other signal processing commands that are applied that are not explicitly stated in the program or done by me]
       
2. Reads 2D spectra and takes intervals based on where a peak for a molecule is creating the most noise
   - can't lie, I have no idea how this would be created. The confusing part is that every molecule has a different looking peak, and so I'm not sure if this would turn into a ML project that can dictate which parts are noise and which parts are actual molecules. Perhaps this would simply be dictated by giving a lower limit of height- anything above that height would most likely be a notable peak.
     
3. After taking different peaks, they must be cleaned of any excess noise, and then integrated

4. Yippeeeee

This is a really confusing project simply because so much of the manual data processing usually requires special attention to small details or discrepencies in the data (usually stemming from mistakes or impurities in the data collection process). chat usually gives a good outline/structure for what the script will look like, but the rest will need to be developed. 
