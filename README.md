# GNU PRACTISE 


## Introduction



![image](https://github.com/user-attachments/assets/777310eb-111c-4df1-96bf-cdaeba72e1ad)

We go with digital communication as it is is more reliable than analog communiation. when we have noise in the system it is easier to decode a bit 0 or 1 rather than decode the whole spectrum of signals that are present while having a signal. It is similar to how analog signal will have all the details of a painting and when scaled down becomes harder to understand whereas digital comms is just distinguishing between black and white. 


# WEEK 1:

</details>
<details>
<summary>EXPERIMENT 1: A simple program  </summary>
<br>


![image](https://github.com/user-attachments/assets/8fc42e1b-b51e-4741-aaf5-1b972c0c111e)

We need sampling as real signals are continous and have value for all infinite time intervals and its not possible for computers to compute all the intervals of time that is needed, so we follow nyquist sample theorem to ensure that there are enough samples to recreate the signals using a dac ( fs >= 2*fm ). 


![image](https://github.com/user-attachments/assets/104a363c-e21f-4c2a-a965-02426b223030)

This is a simple program to show a cos signal being generated using a signal source and being captured using a time sink. we can see that the signal is being sampled at 32k which means that at every 1/32k time interval we take a sample which is shown below

![image](https://github.com/user-attachments/assets/20337750-dd38-4ead-9f7f-6ad589741ba3)

</details>
<details>
<summary>EXPERIMENT 2: Low Pass Filter </summary>
<br>

![image](https://github.com/user-attachments/assets/8f56cc16-7a2d-4c59-997d-012c2016b5fe)
A low pas filter with a cutt off freq of 4500 and a Transition Width of 1000 is being used, so any frequency below 4500 will be passed and anything above will start to diminish, we can see this behaviour by looking at the time and frequency plot below.

![image](https://github.com/user-attachments/assets/e108cd64-359d-4378-a0b4-705088f5f6c6)
here we have no loss of signal, where the output of low pass is with a delay represented by the red signal as it undergoes a small delay due to the low pass signal.

![image](https://github.com/user-attachments/assets/05736335-7fcd-4c94-a6bd-7a3e1d97ea37)

here we have a  loss of the signal due to the freq being at 5000 which is above the low pass filter cut off frequency. Both the time and freq plot show a decline in the power level of the signal.

</details>
<details>
<summary>EXPERIMENT 3: Vectors and Fourier transform of a sinc signal  </summary>
<br>


![image](https://github.com/user-attachments/assets/de584899-8753-4750-b239-1d10eec46b49)

The fourier transform of a sinc(t) signal is a rectangular wave in the freq domain. By following the property of band limiting i.e if the signal is band limited in the freq domain it is infinite in the time domain and vice versa, as we know sinc is infinite in the time domain, we can create band limited signals in the freq domain. The above example of sinc(t) -0.5sinc(t-1) has been done in gnu radio.


To do this we have to first decide on the sample limit i.e 1024 and by taking into the sample rate we can take time intervals from [-512/32,.....511/32] , a vector block is using with the numpy to find the values of the sinc at the different intervals.
![image](https://github.com/user-attachments/assets/42689338-36c1-4ff1-95ac-aecc63dc26fb)


![image](https://github.com/user-attachments/assets/0d0b368b-54e6-47bc-8609-0af289d026a3)


Blue represents the original signal which is the A1*sinc(t) and the red shows the A2*sinc(t-1), and the resultant is shown by the green signal output ( sinc(t) -0.5sinc(t-1) ). as we can see no matter the linear combination of the sinc signals in the time domain, we have a band limited frequncy plot. We have the truncation of the sinc wave which causes the ripples in the freq domain.


</details>
<details>
<summary>EXPERIMENT 4: Windowing   </summary>
<br>

![image](https://github.com/user-attachments/assets/ade04482-ba07-41fb-a220-f48948099fde)

When we operate using in the time domain its impossible to account for the infinite amount of the time and thus we go for windowing where an interval is taken into consideration instead of the whole time domain. In the above figure we can see that the freq lines at the two are not discrete , this is because we are multiplying with a rect window which in the freq domain is a sinc , We can get more discrete signals with increasing the window size.

![image](https://github.com/user-attachments/assets/da4af8e5-a998-4316-9180-e80ad0f8571a)

at f=1000hz, we observe discrete signals along with some noise and will continue to have discrete signals if it fulfils 

f/f2 * Nfft = Int

when f=1010 hz , we do not observe discrete lines untill we increase the window size as shown below:

![image](https://github.com/user-attachments/assets/1a853008-4f80-45fc-8e02-4581b387d807)


![image](https://github.com/user-attachments/assets/6a3286ee-8d72-492b-aa6a-f9017670f0ae)

On increasing the fft window size to 16384 we get more discrete lines in the frequency plot. 

</details>
<details>
<summary>EXPERIMENT 5: complex baseband Representation    </summary>
<br>


![image](https://github.com/user-attachments/assets/4ee6cac2-87aa-446d-ba44-a25d029bb55a)

A baseband signal is a signal that is centered at the dc and passband is a signal that is centered at the carrier freq, This conversion can lead to the duplicate data being transmitted when the signal in the baseband is real signal. We can improve the spectrun usage by using a complex baseband technique where two real signals Ss(t) and Sc(t) are used to create S(t)= Sc(t) + jSs(t).

This allows us to use the complete spectrum , we can also get this passband output by mathematical calculations and come to the result sp(t) = Sc(t)*cos(2*pi*fc*t) - Ss(t)*sin(2*pi*fc*t) , where the Sc(t) is the in-phase componenet and the Ss(t) is the quadrature or out of phase component.

![image](https://github.com/user-attachments/assets/10e766d0-87a4-4263-9927-d27985db16ff)


In GNU radio we can use 2 signal generators to produce two real signals , cos2pi*f0*t and sin2pi*f0*t and make sure f0<< to make them baseband signal approx, We can then use a conv to get the complex baseband representation, 


![image](https://github.com/user-attachments/assets/3a43a801-982a-4f6a-b921-552e11a7a463)

The blue signal represents the complex baseband representation of the two signals i.e cos and sin signals. We see that only signal is present at 1Khz as cos + jsin = e^2*pi*f0*t which has a fourier transform of having an impulse at f0. 

![image](https://github.com/user-attachments/assets/9d2afa0c-5827-4984-83a7-ed3de9447071)

after we get the complex baseband representation of the signal, we need to convert it into passband signal, for this we multiply with a carrier signal of 6Khz and at the end observe the signals at +7khz and -7khz as the carrier is at 6khz and we have the complex baseband signal at 1khz.

![image](https://github.com/user-attachments/assets/17d0bcd2-9ce0-4d21-bfa6-15075b1a5866)


This shows us the converstion of two baseband signals into a complex baseband represenation and then into a passband signal which makes a more efficent use of the available bandwidth.

</details>
<details>
<summary>EXPERIMENT 6:  Up and Down conversion of Complex Baseband Signals   </summary>
<br>

![image](https://github.com/user-attachments/assets/c76be984-3d4b-40e3-bfd7-4c2634b1e792)

We can convert from baseband to passband directly by multiplying the in phase and out of phase components as shown above. In gnu radio we take two baseband signals i.e sinc(t) and sinc^2(t). 
![image](https://github.com/user-attachments/assets/a2c7dfb7-f7eb-4475-8eb1-5b83f34274b2)



The sinc is generated by using a vector source and the Sc(t) is multiplied with a cos and Ss(t) with a sin wave operating at fc . 


![image](https://github.com/user-attachments/assets/c7d01c5c-2de0-4841-8071-3b356e831a3c)

Blue color shows the sinc(t) and the red shows the Sinc^2(t) , we can see that its fourier transform is a rect and a convolution of 2 rects respectively. After the passband conversion, we see that the signal i.e the complex baseband represented signal has been shifted to both the right and left of fc. This is a proper conversion of the complex baseband signal to the passband representaion.


![image](https://github.com/user-attachments/assets/ea9caf27-0c2b-4ff0-893b-ad0e83b8b9c8)


If we want to get back the baseband signal from this passband signal, we need to multiple the passband with a cos to get the Sc(t) comp and a sin to get the Ss(t) comp, we also need to use a low pass filter at fc in order to remove the unwanted components, we can do this since our baseband signal is a dc signal centered at 0. 

![image](https://github.com/user-attachments/assets/810517db-ed75-4fde-a6da-33d971f5e34a)

Output 2 and 4 are the passband output which we will use as reference to get the baseband output, output 1 and 3 can be observed to see that the signal i.e the sinc(t) and sinc^2(t) has been recovered successfully after conversion and we notice a small delay in the time domain as we use a low pass filter. 

This concludes that we use Complex baseband signals to ensure maximum bandwidth usage and we can convert from baseband to passband and vise-versa by multiplying with a cos and sin respectively. We also need to remeber the root2 multiplication to the amplitude ignoring which we wiill get the converted signal with lesser amplitude.

</details>

# WEEK 2:

<details>
<summary>EXPERIMENT 1: Amplitude Shift Keying </summary>
<br>
 
![image](https://github.com/user-attachments/assets/ecbe6bcc-9e87-4bfb-bebf-018f3d095adc)


We are doing Amplitude shift keying where the symbols can take the value from 0,1,2 or 3, For our example we consider a sample rate of 64000 and a symbol rate of 1000 symb/sec. As we have 64000 samples per second, we need to ensure that the symbols last 1ms each, 

Samples per symbol = sample_rate // 1000 = 64

so 64 samples are needed to represent one symbol in this case. we use the interpolation filter to do so with using a filter tap that fills in ones for the empty space in between. 


![image](https://github.com/user-attachments/assets/23f0bec0-6bd7-41ed-8d2b-8e41b5c59beb)

![image](https://github.com/user-attachments/assets/29752d6b-f74b-4656-b279-1b76b52a4e9e)

We can see here the symbols taking the value from 0,1,2 or 3 and having 64 samples representing each of the symbols. This is the baseband representation of the signal and we need to convert to a passband representation using a carrier signal.

![image](https://github.com/user-attachments/assets/dd2439da-49d4-41c3-b47f-4f1895ab5005)

We do the passband coversion by multiplying with a cos signal of fc = 6000 Hz, after this we demodulate by multiplying with a cos and a -sin wave for the i and q compoennts respectively. 
![image](https://github.com/user-attachments/assets/98b46d16-c219-403e-a507-d5ca5336622c)
The above is the demodulated signal and we can see that after low pass we are able to see the input waveform, as we are using only onw real signal we have no quadrature component in the output. We see a delay in the output due to the filter being a practical filter, there are also uneven due to the rectangle baseband signal not being band limited. 
 
<details>
<details>
<summary>EXPERIMENT 2: Phase Shift Keying </summary>
<br>


