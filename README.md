```mermaid
flowchart TB

%% ===== Backbone (signal flow spine) =====
sp1[Source];
sp2[Coding];
sp3[Modulation];
sp4[Sync];
sp5[RF Frontend];
sp6[Antenna];
sp7[Channel];
sp8[Receiver];
sp9[Quality];
sp10[Operations];

sp1 --> sp2;
sp2 --> sp3;
sp3 --> sp4;
sp4 --> sp5;
sp5 --> sp6;
sp6 --> sp7;
sp7 --> sp8;
sp8 --> sp9;
sp9 --> sp10;

%% ===== Topics anchored to the backbone =====
fourier[Fourier Transform];
awgn[AWGN kTB NF];
cohbw[Coherence BW Bc];
modfilt[Mod Demod Filter];
mfdet[Matched Filter Decision];
pulse[Pulse Shaping RC RRC FTN];
fmcapt[FM Capture Pre Deemph];
linecode[Line Coding NRZ RZ Manchester AMI];
lbudget[Link Budget MDS SNR];
txpower[TX Power FSPL Ant Gain];
fresnel[Fresnel Zone];
veldisp[Velocity Dispersion];
iono[Ionosphere LUF MUF FOT];
txline[Tx Line Impedance];
match[Impedance Match Verify];
distless[Distortionless R L G C];
rxstruct[Receiver Arch RF Basics];
pll[PLL];
superhet[Double Superhet Rx Figures];
rffilt[RF Filter Q BW Ripple];
spectrum[Spectrum Analyzer];
evm[EVM];
imd3[IMD3];
dpcm[DPCM];
psk8[8 PSK Design];
eloran[e Loran];

%% anchor to spine
sp1 --- linecode;
sp1 --- dpcm;
sp1 --- fourier;

sp2 --- psk8;

sp3 --- modfilt;
sp3 --- pulse;
sp3 --- fmcapt;

sp4 --- pll;

sp5 --- rffilt;
sp5 --- rxstruct;
sp5 --- superhet;
sp5 --- txline;

sp6 --- fresnel;

sp7 --- awgn;
sp7 --- cohbw;
sp7 --- veldisp;
sp7 --- iono;

sp8 --- mfdet;
sp8 --- match;

sp9 --- evm;
sp9 --- imd3;
sp9 --- spectrum;

sp10 --- lbudget;
sp10 --- txpower;

%% ===== Cross-relations among topics (key links) =====
fourier --> pulse;
fourier --> rffilt;
awgn --> evm;
awgn --> lbudget;
cohbw --> mfdet;
pulse --> mfdet;
linecode --> pll;
psk8 --> modfilt;
modfilt --> mfdet;
mfdet --> evm;
fmcapt --> evm;
txline --> match;
match --> evm;
distless --> txline;
superhet --> evm;
rffilt --> spectrum;
imd3 --> spectrum;
imd3 --> evm;
txpower --> lbudget;
fresnel --> lbudget;
iono --> lbudget;
veldisp --> cohbw;
eloran --> pll;
eloran --> lbudget;
