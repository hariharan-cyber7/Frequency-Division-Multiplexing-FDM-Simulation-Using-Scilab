# Frequency-Division-Multiplexing-FDM-Simulation-Using-Scilab

# Aim
To simulate Frequency Division Multiplexing (FDM) using Scilab by generating multiple sinusoidal signals of different frequencies,
multiplexing them into a single composite signal, and then performing demultiplexing to extract the original signals.

# Theory
Frequency Division Multiplexing (FDM) is a technique where multiple signals are transmitted simultaneously over a single communication channel.
Each signal is allocated a unique frequency band, allowing them to coexist without interference.

# SCILAB Code
```sci
clc; clear; close;
fs=80000; N=floor(0.05*fs); t=(0:N-1)/fs;
fm=[436 446 456 466 476 486];
fc=[4360 4460 4560 4660 4760 4860];
Am=[5.6 5.7 5.8 5.9 6 6.1];
Ac=[11.4 11.5 11.7 11.8 12 12.2];
num=length(fm);
for i=1:num
    m(i,:)=Am(i)*sin(2*%pi*fm(i)*t);
end
fdm=zeros(1,N);
for i=1:num
    fdm = fdm + Ac(i)*cos(2*%pi*fc(i)*t).*m(i,:);
end
function h=FIR(fc1,fc2,fs,M,mode)
    n=-M:M; L=length(n);
    x1=2*fc1*n/fs; x2=2*fc2*n/fs;
    s1=ones(1,L); s2=ones(1,L);
    for k=1:L
        if x1(k)<>0 then s1(k)=sin(%pi*x1(k))/(%pi*x1(k)); end
        if x2(k)<>0 then s2(k)=sin(%pi*x2(k))/(%pi*x2(k)); end
    end
    lp1=(2*fc1/fs)*s1; lp2=(2*fc2/fs)*s2;
    w=(0.54-0.46*cos(2*%pi*(n+M)/(2*M)));
    if mode==1 then h=lp1.*w;
    else h=(lp2-lp1).*w; end
    h=h/sum(h);
endfunction
M=300;
for i=1:num
    bp=FIR(fc(i)-600,fc(i)+600,fs,M,2);
    iso=conv(fdm,bp,"same");
    mix=iso.*cos(2*%pi*fc(i)*t);
    lp=FIR(800,0,fs,M,1);
    demod(i,:)= (2/Ac(i))*conv(mix,lp,"same");
end
scf(1); clf;
for i=1:num subplot(num,1,i); plot(t,m(i,:)); end
scf(2); clf; plot(t,fdm);
scf(3); clf;
for i=1:num subplot(num,1,i); plot(t,demod(i,:)); end
```

# Output image
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/09450b55-4bd3-43b9-8657-22ff24eba04b" />
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/83572359-0b0d-4ccf-a594-4f067d4499a5" />
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/9a4ad1da-cfe3-42ab-aea0-4016110a8acc" />

# Tabulation:


# Result
FDM was successfully simulated. The six input signals were combined into one composite signal and later recovered correctly through demultiplexing using Scilab.
