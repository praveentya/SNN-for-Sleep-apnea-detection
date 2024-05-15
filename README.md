# SNN-for-Sleep-apnea-detection
A spiking neural network module, tempotron, for the classification of sleep apnea detection 
Artificial neural networks that closely mimic natural neural networks are known as spiking neural networks (SNNs).
 The tempotron: a neuron that learns spike timing-based decisions

Learning real-world stimuli by single-spike coding and tempotron rule
Work in spiking neurons:

When a neuron accepts a stimulant from a pre-neuron, it's stored in the neuron. As long as the stimulation accessed exceeds a threshold of neuron, the neuron generates a spike that passes to the post-neuron. After the spike, the neuron "sleeps" for a while, and its storage value returns to rest potential(may be zero). The neuron stay silent for a period of time, within the interval don't accept any input stimulate.

A neuron accepts all the input stimulated from pre-synaptic neurons, store the stimulates in its potential,

P(t)=∑_(n=1)^M▒v_n  ∑_(t_n^i)▒〖S(t-t_n^i )+P_rest 〗

s: kernel function, value located in [0, 1]. The output of K represents the contribution of spiking happening at n_i.

The latest spiking occurs in t_i, and then the contribution of that spiking during the current timestep t is s(t - n_i). 
S(t-t_n^i )=P_0 [exp(-(t-t_n^i)/γ_a )-xp(-(t-t_n^i)/γ_b )]            
![image](https://github.com/praveentya/SNN-for-Sleep-apnea-detection/assets/48126236/22937fc8-edc3-4e59-a870-050dec86b12c)

In this formula, after spiking occurs, the Kernel function becomes smaller as time goes forward, and the influence of spiking t_i decreases with time. tou_m and tou_s are hyperparameters.

P0 is the normalization function, which limits the kernel function value to 0 and 1. In this formula, t_i must be less than t, because only the spiking generated in the past will contribute to the membrane potential.

After the membrane potential triggers spiking, the neuron will enter a period of "refractory period", and the potential will return to the reset voltage P_rest.

The output of the Spiking neuron is only "triggered" or "not triggered." If you want to use SNN to output multiple categories: 1. Use binary encoding and perform binary decode on the output neuron to generate a decimal output value. For example, five output neurons can be used to represent binary output. If the output is 00000, it represents 1, and 00010 represents 2.

In this simple implementation, two neurons are used to represent the two categories. When the neuron representing a category generates a spike, it indicates that the sample is of that category. Other classes of output neurons are inhibited. We use this method to train a number of binary classifiers equal to the number of categories so that the SNN can distinguish three categories.
Model training: If the sample is category B and the output neuron A emits a pulse, the synaptic weight connected to this neuron A needs to update the weight. The training goal is to control the membrane potential of output neuron A. Conversely, the goal is to enhance the membrane potential of the output neuron.

Input encoding: SNN treats input information as nerve impulses, so we must encode the numerical value into the input stimulus in time units. The Gaussian function is used as the encoding function here. For each input value, each Gaussian neuron is a Gaussian function separated by a small distance.
![image](https://github.com/praveentya/SNN-for-Sleep-apnea-detection/assets/48126236/ebecb679-8141-45bc-ad4c-f3813c715962)
