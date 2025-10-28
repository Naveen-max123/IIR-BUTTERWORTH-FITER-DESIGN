# EXP 3 : IIR-BUTTERWORTH-FITER-DESIGN

## AIM: 

 To design an IIR Butterworth filter  using SCILAB. 

## APPARATUS REQUIRED: 
PC installed with SCILAB. 

## PROGRAM (LPF): 
```
clc ;  

close ;  

wp=input('Enter the pass band frequency (Radians )= ' );  
ws=input('Enter the stop band frequency (Radians )= ' );  
alphap=input( ' Enter the pass band attenuation (dB)=' );  
alphas=input( ' Enter the stop band attenuation(dB)=' );  

T=input('Enter the Value of sampling Time='); 
omegap=(2/T)*tan(wp/2);  
disp(omegap,'omegap=');  
omegas=(2/T)*tan(ws/2);  
disp(omegas,'omegas=');    
N=log10(((10^(0.1*alphas))-1)/((10^(0.1*alphap))-1))/(2*log10(omegas/omegap));  
disp(N,'N='); 
N=ceil(N);  
disp(N,'Round off value of N=');  
omegac=omegap/(((10^(0.1*alphap)) -1)^(1/(2* N)));  
disp(omegac,'omegac=');  
disp('Normalised Analog LPF Transfer function H(S)=');  
hs_Normalised = analpf(N,'butt',[0,0],1); 
disp(hs_Normalised);  
disp('Analog LPF Transfer function H(S)=');  
hs= analpf(N,'butt',[0,0],omegac);  
disp(hs);  
z=poly(0,'z'); 
Hz=horner(hs,(2/ T)*((z -1)/(z+1))) 
disp('Digital LPF Transfer function H(Z)=');  
disp(Hz);  
HW=frmag(Hz,512);  
w=0:%pi/511:%pi ;  
plot(w/%pi,abs(HW));  
xlabel(' Normalized Digital Frequency w');  
ylabel('Magnitude '); 
title(' Frequency Response of Butterworth IIR LPF');
```
## PROGRAM (HPF): 
```
clc;
close;
wp = input('Enter the pass band frequency (Radians )= ');
ws = input('Enter the stop band frequency (Radians )= ');
alphap = input('Enter the pass band attenuation (dB)= ');
alphas = input('Enter the stop band attenuation (dB)= ');
T = input('Enter the Value of sampling Time= ');

// Pre-warping (Bilinear Transformation)
omegap = (2/T) * tan(wp/2);
disp(omegap, 'omegap=');
omegas = (2/T) * tan(ws/2);
disp(omegas, 'omegas=');

// Order of the filter
N = log10(((10^(0.1*alphas))-1) / ((10^(0.1*alphap))-1)) / (2*log10(omegas/omegap));
disp(N,'N=');
N = ceil(N);
disp(N,'Round off value of N=');

// Cut off frequency
omegac = omegap / (((10^(0.1*alphap))-1)^(1/(2*N)));
disp(omegac,'omegac=');

// Normalised Analog LPF Transfer function
disp('Normalised Analog LPF Transfer function H(S)=');
hs_Normalised = analpf(N,'butt',[0,0],1);
disp(hs_Normalised);

// Analog LPF Transfer function
disp('Analog LPF Transfer function H(S)=');
hs = analpf(N,'butt',[0,0],omegac);
disp(hs);

s = poly(0,'s');
hpf_s = horner(hs, omegac/s);   // substitute s → omegac/s
disp('Analog HPF Transfer function H(S)=');
disp(hpf_s);

// Bilinear Transformation to Digital
z = poly(0,'z'); // Defining variable z
Hz = horner(hpf_s,(2/T)*((z-1)/(z+1))); 
disp('Digital HPF Transfer function H(Z)=');
disp(Hz);

// Frequency Response
HW = frmag(Hz,512);
w = 0:%pi/511:%pi;
plot(w/%pi, abs(HW));

xlabel(' Normalized Digital Frequency w');
ylabel('Magnitude');
title(' Frequency Response of Butterworth IIR HPF');
```

## OUTPUT (LPF) : 
<img width="1672" height="997" alt="image" src="https://github.com/user-attachments/assets/67e9532a-58da-42f6-9de7-7995b70d3f59" />
<img width="1677" height="995" alt="image" src="https://github.com/user-attachments/assets/633aeeee-ee2b-4df4-ade2-d8a62a1a10fd" />
<img width="1676" height="996" alt="image" src="https://github.com/user-attachments/assets/f39815c1-5b1c-4282-9ccb-556ac3f26f85" />

## OUTPUT (HPF) : 
<img width="1676" height="994" alt="image" src="https://github.com/user-attachments/assets/ac8222b8-a22d-41a5-8296-849713fa73d7" />
<img width="1674" height="995" alt="image" src="https://github.com/user-attachments/assets/1576ec5f-fc96-413d-a5d4-32e71629ddbb" />
<img width="1680" height="999" alt="image" src="https://github.com/user-attachments/assets/86966748-6bde-4471-b847-7bd8cb64da50" />

## RESULT: 
Thus, the design of an IIR Butterworth filter(LPF/HPF) using SCILAB is sucessfully executed and output is verified.
