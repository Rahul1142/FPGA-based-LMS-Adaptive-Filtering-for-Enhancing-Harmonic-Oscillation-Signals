# FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals
The objective of this project was to implement an FPGA-based LMS adaptive filter  to filter out noise from a sinusoidal signal.

The project aimed to demonstrate the  effectiveness of the LMS algorithm in filtering out noise from a signal. 

Implementation: Develop and deploy an adaptive filtering system using the LMS algorithm within an FPGA architecture. 

Demonstration: Showcase the adaptability and real-time processing capabilities of the LMS algorithm in reducing noise interference from a sinusoidal signal.

Validation: Verify the performance of the adaptive filter by fine-tuning parameters and refining filter coefficients to achieve an output closely resembling
a pure sinusoidal wave, considering the limitations and intricacies of FPGA implementations. 

Analysis: Assess the effectiveness of the adaptive filter in enhancing signal fidelity by comparing the filtered output with the original pristine signal and evaluating the 
degree of noise reduction achieved.

The project aims to not only implement the theoretical concepts but also validate and demonstrate their practical effectiveness, emphasizing the potential of FPGA-based
adaptive filters in real-world signal processing applications. 


(A) Signal Generation and Manipulation: 

The project was initiated by generating an original sinusoidal signal using MATLAB. 
A base sine wave function was generated, and Gaussian noise was added to 
simulate real-world conditions, producing a noisy signal. This initial signal was 
stored for further use in FPGA implementation. 

Implementation of LMS function in MATLAB:

% Function implementing the LMS (Least Mean Squares) 
algorithm function [w,e,yn] = my_LMS(xn,dn) 

k=128;    % Filter length 
L=length(xn); % Length of input signal
yn = zeros(1,L); % Initialize output signal
yn(1:k) = xn(1:k); % Copy initial part of input 
to output w = zeros(1,k); % Initialize filter weights
e = zeros(1,L); % Initialize error signal
% Calculate maximum eigenvalue for step 
size adjustment fe = max(eig(xn*xn.')); 
u = 2*(1/fe); % Update step size based on the maximum eigenvalue

% LMS algorithm 
iterations for i = (k+1):L 
XN = xn((i-k+1):(i)); % Extract current 
window of input yn(i) = w * XN'; % Compute 
output using current weights
e(i) = dn(i) - yn(i); % Calculate error between output 
and desired signal w = w + u * e(i) * XN; % Update 
filter weights using LMS formula
end
end

  Let's call the above function: To quantize the generated sine wave and the noisy sine wave, the quantized data will be used later in Vivado.


  //Code of Matlab through image

  ![image](https://github.com/Rahul1142/FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals/assets/100791352/56bcabc4-2009-4d94-b7c5-3d613c321e08)
  
Let's call the above function: To quantize the generated sine wave and the noisy sine wave, the quantized data will be used later in Vivado.

![image](https://github.com/Rahul1142/FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals/assets/100791352/d06e2c23-d4ec-423b-ae54-82c2ab217115)





(B) Signal Processing and Filtering: 
The FPGA-based LMS adaptive filter required specific parameters for implementation. The step factor, crucial in the LMS algorithm, was set to a 
constant value of 3 to ensure convergence. Additionally, an iterative approach was employed to fine-tune the filter's coefficient for optimal noise reduction while 
preserving the signal's integrity. 

(C) Data Capture and Analysis: 
Time domain waveforms of the original signal, the noisy signal, and the output after LMS adaptive filtering were generated and plotted. These plots facilitated the 
visualization of the filtering process, showcasing the noise reduction and the similarity/differences between the filtered and original signals. Notably, the error 
between the original signal and the LMS-filtered signal was computed and plotted to quantify the filtering efficacy. 

(D) File Preparation for FPGA Implementation: 
The generated noisy signal and the original sinusoidal signal, along with relevant filter coefficients, were saved in suitable file formats compatible with the FPGA 
platform. This preparatory step ensured that the signals and necessary parameters were available for integration into the FPGA environment. 

(e) FPGA Implementation and Verification: 
Utilizing Vivado, a comprehensive FPGA development environment, the project was simulated and implemented in RTL (Register-Transfer Level). The correctness 
and functionality of the designed filter were verified through simulations and by analyzing the outputs against expected results. 
This section focuses on explaining the steps taken to generate, manipulate, and prepare the signals and parameters necessary for the FPGA-based LMS adaptive 
filter implementation.
It also highlights the tools and methodologies used for data analysis and verification, which are essential in validating the filter's effectiveness.

  Results 
The implementation of the FPGA-based LMS adaptive filter yielded insightful outcomes. The recorded observations from the experiment are detailed below:

(A)Signal Analysis 
The waveform analysis of the signal progression through the filter revealed several crucial aspects: 

Input Data Signal: The original sinusoidal signal generated in MATLAB exhibited the expected sinusoidal behaviour. 

Mathematical Expression: x(t)=A⋅sin(2πft+ϕ) 

Output Data Signal: The signal after adaptive filtering using the LMS algorithm showcased a reduction in noise components but deviated slightly 
from an ideal sinusoidal wave due to implementation parameters. Expected Signal Data: The anticipated signal after filtering, when compared to 
the original clean sinusoidal signal, showed remarkable similarity, albeit not precisely identical due to implementation limitations.

(B)Deviations and Causes 
The deviation of the filtered signal from an ideal sinusoidal wave was primarily attributed to two factors:[11] 

Step Factor: The set value of the step factor significantly impacted the convergence rate and the accuracy of the filtered output. 

Mathematical Representation: μ=3 

Simulation Time: Limitations in simulation time affected the fidelity of the filtered output, preventing it from precisely replicating the clean sinusoidal 
wave.

(C)Verification and Validation 
The FPGA implementation and simulation using Vivado were successfully executed and verified against the expected results. While the output wasn't a 
perfect sine wave due to the aforementioned factors, the algorithm's efficacy in noise reduction was discernible. 

(D) MATLAB Simulation Results 

![image](https://github.com/Rahul1142/FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals/assets/100791352/ea59e61e-6484-4bf1-a7a7-670aef1fd829)

(E) FPGA Simulation Results 

![image](https://github.com/Rahul1142/FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals/assets/100791352/16ed6c22-dde2-4a8d-9365-518d0bfc4733)

![image](https://github.com/Rahul1142/FPGA-based-LMS-Adaptive-Filtering-for-Enhancing-Harmonic-Oscillation-Signals/assets/100791352/91bbe900-40a5-4ef2-9fa5-225c57c9ee65)

The waveform of the input data signal, output data signal, and the expected signal data after passing through the filter (which is very close) were observed.
The output was not a perfect sine wave due to the step factor and simulation time. 

Conclusion 

The FPGA-based LMS adaptive filter project was successfully implemented and verified. The project demonstrated the effectiveness of the LMS algorithm in 
filtering out noise from a signal. The main challenges faced during the implementation of the project were related to the FPGA implementation,
which was addressed by setting the step factor to a constant of 3 and iterating the coefficient of the filter to a perfect coefficient. 

In conclusion, the FPGA-based LMS adaptive filter project has achieved its objectives in showcasing the effectiveness of the LMS algorithm in noise reduction 
from a sinusoidal signal. Despite encountering challenges primarily associated with FPGA implementation, strategic adjustments such as setting the step factor to 
a constant value and refining the filter coefficient were made to mitigate these issues. 

The project's success was validated through comprehensive experimental setups, including MATLAB-generated signals, the introduction of Gaussian noise, and the 
subsequent filtering via the LMS algorithm. Although the output signal didn't perfectly replicate the sinusoidal waveform due to constraints like step factor and 
simulation time, the outcomes closely approximated the expected results. 

This project not only emphasized the application of the LMS algorithm in adaptive filtering but also highlighted the significance of addressing FPGA-specific hurdles 
in signal-processing implementations. The successful verification of the FPGA implementation using Vivado solidifies the practicality of this approach. 

Moving forward, potential enhancements could involve further optimization of FPGA-specific parameters and refining the algorithm to achieve even more precise 
noise reduction without distorting the original signal. Overall, this project contributes to the understanding and practical implementation of adaptive filtering 
techniques, specifically highlighting the prowess of the LMS algorithm in real-time signal processing scenarios. 





























