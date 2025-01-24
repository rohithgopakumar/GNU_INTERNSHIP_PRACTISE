# GNU PRACTISE INTERNSHIP


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
<summary>EXPERIMENT 5:    </summary>
<br>
