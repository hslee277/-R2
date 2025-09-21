flowchart TB

%% ---------- Nodes (topics you gave)
fourier["Fourier Transform"];
awgn["AWGN (kTB, NF)"];
coh_bw["Coherence BW (Bc)"];
mod_filt["Mod/Demod & Filtering"];
mf_detect["Matched Filter & Decision"];
pulse["Pulse Shaping (RC/RRC) & FTN"];
fm_capture["FM Capture & Pre/De-emph"];
linecode["Line Coding (NRZ/RZ/Manchester/AMI)"];
linkbudget["Link Budget (MDS, SNR, kTB, NF)"];
txpower["TX Power (FSPL, Ant Gain)"];
fresnel["Fresnel Zone"];
vel_disp["Velocity/Dispersion & Mitigation"];
ionosphere["Ionosphere (LUF/MUF/FOT)"];
txline["Tx Line & Impedance"];
match["Impedance Match & Verification"];
distless["Distortionless Condition (R/L = G/C)"];
rx_struct["Receiver Structure & RF Basics"];
pll["PLL (Arch & Principle)"];
superhet["Double Superhet & 4 Rx Figures"];
rffilter["RF Filter (Q, BW, Ripple)"];
spectrum["Spectrum Analyzer & Settings"];
evm["EVM"];
imd3["IMD (3rd)"];
dpcm["DPCM"];
psk8["8-PSK Design"];
eloran["e-Loran"];

%% ---------- Related nodes (added to enrich relationships)
ber["BER"];
ebn0["Eb/N0"];
isi["ISI"];
equalizer["Equalizer (ZF/MMSE/DFE)"];
diversity["Diversity (MRC/SC)"];
mimo["MIMO / Beamforming"];
ofdm["OFDM + CP"];
gi["Guard Interval (GI)"];
lna["LNA"];
mixer["Mixer"];
pa_dpd["PA + DPD"];
duplexer["Duplexer (SAW/BAW)"];
pathloss["Path-loss Models"];
doppler["Doppler / Tc"];
adc_dac["ADC / DAC"];
agc["AGC"];
cdr["CDR / Timing Recovery"];
afc["AFC"];
chan_est["Channel Estimation"];
acpr["ACPR / ACLR"];

%% ---------- Core relations
awgn --> ebn0;
awgn --> linkbudget;
awgn --> evm;
awgn --> ber;

ebn0 --> ber;
evm --> ber;

coh_bw --> isi;
pulse --> isi;
ofdm --> gi;
gi --> isi;

isi --> mf_detect;
isi --> evm;

equalizer --> isi;
diversity --> awgn;
mimo --> awgn;

fourier --> pulse;
fourier --> rffilter;
fourier --> spectrum;

linecode --> cdr;
cdr --> mf_detect;

mod_filt --> mf_detect;
mf_detect --> evm;

dpcm --> linecode;

psk8 --> mod_filt;
psk8 --> mf_detect;
psk8 --> evm;

fm_capture --> evm;

%% ---------- RF chain & impairments
rx_struct --> superhet;
rx_struct --> pll;
rx_struct --> rffilter;

lna --> rx_struct;
mixer --> rx_struct;
pa_dpd --> imd3;
duplexer --> rffilter;

imd3 --> acpr;
acpr --> spectrum;
rffilter --> acpr;

pll --> evm;
superhet --> evm;

txline --> match;
match --> evm;

distless --> txline;

%% ---------- Link budget & propagation
txpower --> linkbudget;
fresnel --> pathloss;
pathloss --> linkbudget;

ionosphere --> pathloss;
doppler --> coh_bw;

vel_disp --> coh_bw;

linkbudget --> evm;
linkbudget --> ber;

%% ---------- Measurement loop
spectrum --> acpr;
spectrum --> rffilter;

%% ---------- Services / examples
eloran --> pll;
eloran --> linkbudget;
