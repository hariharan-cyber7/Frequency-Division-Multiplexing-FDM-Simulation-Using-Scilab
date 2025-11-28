# Frequency-Division-Multiplexing-FDM-Simulation-Using-Scilab

# Aim
To simulate Frequency Division Multiplexing (FDM) using Scilab by generating multiple sinusoidal signals of different frequencies,
multiplexing them into a single composite signal, and then performing demultiplexing to extract the original signals.

# Theory
Frequency Division Multiplexing (FDM) is a technique where multiple signals are transmitted simultaneously over a single communication channel.
Each signal is allocated a unique frequency band, allowing them to coexist without interference.

# SCILAB Code
```sci
t = linspace(0, 1, 1000);
freqs = [5, 5.5, 6, 6.5, 7, 7.5];

signals = zeros(6, length(t));
for i = 1:6
    signals(i, :) = sin(2 * %pi * freqs(i) * t);
end

fdm_signal = zeros(1, length(t));
for i = 1:6
    fdm_signal = fdm_signal + signals(i, :);
end

demux_signals = zeros(6, length(t));
for i = 1:6
    demux_signals(i, :) = fdm_signal .* sin(2 * %pi * freqs(i) * t);
end

scf(1);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, signals(i, :));
    title('Original Signal f=' + string(freqs(i)));
end


scf(2);
clf;
plot(t, fdm_signal);
title("FDM Signal");

scf(3);
clf;
for i = 1:6
    subplot(3,2,i);
    plot(t, demux_signals(i, :));
    title('Demultiplexed Signal f=' + string(freqs(i)));
end
```

# Output image
<img width="762" height="696" alt="image" src="https://github.com/user-attachments/assets/2c31d985-2677-403f-807c-935f625cf133" />
<img width="758" height="714" alt="image" src="https://github.com/user-attachments/assets/552e12b0-2f9a-4137-92d5-b5f9275a92ce" />
<img width="757" height="716" alt="image" src="https://github.com/user-attachments/assets/3d957e71-a819-4e74-8fab-4c77db6b18aa" />

# Tabulation:


# Result
FDM was successfully simulated. The six input signals were combined into one composite signal and later recovered correctly through demultiplexing using Scilab.
