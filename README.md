```mermaid
flowchart TB

%% ===== 뼈대(신호 흐름 Spine) =====
sp1[원천(소스)];
sp2[코딩];
sp3[변조];
sp4[동기];
sp5[RF 프런트엔드];
sp6[안테나];
sp7[채널];
sp8[수신기];
sp9[품질·측정];
sp10[운용·계획];

sp1 --> sp2;
sp2 --> sp3;
sp3 --> sp4;
sp4 --> sp5;
sp5 --> sp6;
sp6 --> sp7;
sp7 --> sp8;
sp8 --> sp9;
sp9 --> sp10;

%% ===== 토픽(한글 라벨) =====
fourier[푸리에 변환];
awgn[AWGN (kTB, NF)];
cohbw[상관대역폭(Bc)];
modfilt[변조·검파·필터링];
mfdet[정합필터링 & 데이터 판정];
pulse[펄스 성형(RC/RRC) & FTN];
fmcapt[FM 포획효과 & Pre/De-emph];
linecode[라인코딩(NRZ/RZ/맨체스터/AMI)];
lbudget[링크버짓(MDS, SNR, kTB, NF)];
txpower[송신전력(FSPL, 안테나 이득)];
fresnel[프레넬 존];
veldisp[전파 속도·분산과 대책];
iono[전리층 특성주파수(LUF/MUF/FOT)];
txline[전송선로·임피던스];
match[임피던스 정합과 확인];
distless[무왜곡 전송 조건(R/L=G/C)];
rxstruct[수신기 구조·RF 기초];
pll[PLL(구성과 원리)];
superhet[더블 슈퍼헤테로다인 & 수신기 4대 특성];
rffilt[RF 필터(Q, BW, Ripple)];
spectrum[스펙트럼 분석기(원리·설정)];
evm[EVM(오차벡터 크기)];
imd3[IMD(3차)];
dpcm[DPCM];
psk8[8-PSK 설계];
eloran[e-Loran];

%% ===== 뼈대에 앵커링 =====
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

%% ===== 핵심 상호 연관 =====
fourier --> pulse;
fourier --> rffilt;

awgn --> evm;
awgn --> lbudget;

cohbw --> mfdet;
veldisp --> cohbw;

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

eloran --> pll;
eloran --> lbudget;
