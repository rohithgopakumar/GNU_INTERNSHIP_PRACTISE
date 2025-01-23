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
<summary>EXPERIMENT 3:  </summary>
<br>


