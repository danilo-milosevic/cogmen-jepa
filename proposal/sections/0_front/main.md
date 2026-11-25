\begin{center}
\begin{tabular}{m{3cm} m{9cm} m{3cm}}
    \centering\includegraphics[width=2.5cm]{figures/unis.png}
    &
    \centering
    \large УНИВЕРЗИТЕТ У НИШУ\\
    \large ЕЛЕКТРОНСКИ ФАКУЛТЕТ У НИШУ
    &
    \centering\includegraphics[width=2.5cm]{figures/elfak.png}
\end{tabular}
\vspace{3cm}

{\huge\textbf{COGMEN-JEPA}} \\
\vspace{.5cm}
{\textbf{Предиктивно самонадгледано учење мултимодалних репрезентација за препознавање емоција у конверзацији}}\\
\vspace{1cm}

Мастер рад - студијско истраживачки рад\\
\vspace{.5cm}
Студијски програм: Вештачка интелигенција и машинско учење

\end{center}

\vfill

```{=latex}
\begin{center}
\begin{tabular}{>{\centering\arraybackslash}m{0.45\textwidth} >{\centering\arraybackslash}m{0.45\textwidth}}
Студент: & Ментор: \\[0.8cm]
\begin{tabular}{c}Данило Милошевић,\\ број индекса 1732\end{tabular} &
\begin{tabular}{c}Проф. др Јелена Николић\end{tabular} \\
\end{tabular}
\par\vspace{2.5cm}
Ниш, октобар 2026. године
\end{center}
\thispagestyle{empty}
```


```{=latex}
\newpage
\thispagestyle{empty}
\noindent Универзитет у Нишу\par\medskip
\noindent Електронски факултет\par
\vspace{0.9cm}
\noindent{\bfseries ПРЕДИКТИВНО САМОНАДГЛЕДАНО УЧЕЊЕ МУЛТИМОДАЛНИХ РЕПРЕЗЕНТАЦИЈА ЗА ПРЕПОЗНАВАЊЕ ЕМОЦИЈА У КОНВЕРЗАЦИЈИ\par}
\vspace{0.6cm}
\noindent{\bfseries\begin{english}PREDICTIVE SELF-SUPERVISED LEARNING OF MULTIMODAL REPRESENTATIONS FOR EMOTION RECOGNITION IN CONVERSATION\end{english}\par}
\vspace{0.8cm}
\noindent Мастер рад\par\smallskip
\noindent Студијски програм: Вештачка интелигенција и машинско учење\par\smallskip
\noindent Студент: Данило Милошевић, бр. инд. 1732\par\smallskip
\noindent Ментор: Проф. др Јелена Николић\par
\vspace{1cm}
\noindent\underline{Задатак}: \textit{Задатак овог мастер рада је да испита да ли се перформансе модела \textit{COGMEN} за мултимодално препознавање емоција у конверзацији могу побољшати самонадгледаним претренирањем његовог контекст екстрактора по принципу архитектуре \textit{JEPA}. Потребно је анализирати модел \textit{COGMEN} и методе самонадгледаног учења, предложити начин маскирања модалитета и изговора у разговору, као и експерименте којима се проверава да ли претренирање доводи до бољих репрезентација изговора, веће отпорности на недостајуће модалитете и могућности предвиђања емоција будућих изговора. Додатно, потребно је анализирати начин на који модел доноси одлуке.}\par
\vspace{0.9cm}
\noindent Датум пријаве рада:\par\smallskip
\noindent Датум предаје рада:\par\smallskip
\noindent Датум одбране рада:\par
\vspace{0.9cm}
\hfill\begin{minipage}{0.6\textwidth}
Комисија за оцену и одбрану:\par\vspace{0.8cm}
\noindent\rule{\linewidth}{0.4pt}\par
1. Проф. др Јелена Николић, Председник Комисије\par\vspace{0.8cm}
\noindent\rule{\linewidth}{0.4pt}\par
2.\par\vspace{0.8cm}
\noindent\rule{\linewidth}{0.4pt}\par
3.
\end{minipage}

\newpage
\begin{center}
ПРЕДИКТИВНО САМОНАДГЛЕДАНО УЧЕЊЕ МУЛТИМОДАЛНИХ РЕПРЕЗЕНТАЦИЈА ЗА ПРЕПОЗНАВАЊЕ ЕМОЦИЈА У КОНВЕРЗАЦИЈИ\par\vspace{1cm}
{\bfseries САЖЕТАК}
\end{center}
\vspace{0.5cm}

Препознавање емоција у конверзацији је задатак у коме је потребно одредити емоцију сваког изговора у разговору, при чему емоција зависи од онога што је речено, начина на који је речено, израза лица говорника и претходног тока разговора. Модел \textit{COGMEN} овај проблем решава граф неуронском мрежом над разговором, при чему контекст екстрактор, заснован на трансформер енкодеру, на основу унапред израчунатих текстуалних, аудио и видео обележја генерише репрезентације изговора. Овај енкодер се, међутим, тренира искључиво над лабелама емоција, док су скупови података за препознавање емоција мали.

У овом раду предлаже се самонадгледано претренирање контекст екстрактора модела \textit{COGMEN} по принципу архитектуре \textit{JEPA} (\textit{Joint Embedding Predictive Architecture}). Током претренирања маскирају се поједини модалитети изговора или будући изговори, а модел на основу видљивог дела разговора предвиђа репрезентације маскираних делова, које генерише циљни енкодер чије се тежине ажурирају експоненцијалним покретним просеком. Након претренирања енкодер се користи као контекст екстрактор модела \textit{COGMEN}, који се затим тренира над лабелама емоција.

Постављене су три хипотезе: да претренирање доводи до бољих репрезентација изговора и бољег разликовања сличних емоција, да маскирање модалитета чини модел отпорнијим на недостајуће модалитете и да маскирање у времену омогућава предвиђање емоција будућих изговора. Хипотезе ће се проверавати над скуповима података \textit{IEMOCAP} и \textit{CMU-MOSEI}, пондерисаном и макро F1 мером, поређењем са оригиналним моделом \textit{COGMEN} и са генеративним претренирањем као контролним експериментом. Поред тога, предвиђена је анализа начина на који модел доноси одлуке, на основу \textit{attention} коефицијената граф трансформера, аблације по типу релације и методе \textit{GNNExplainer}, као и резервни приступ у коме модел, помоћу \textit{gating} механизма, комбинује претрениране и оригиналне репрезентације.

\vspace{0.5cm}
\noindent\textbf{Кључне речи:} препознавање емоција у конверзацији, мултимодално учење, самонадгледано учење, \textit{JEPA}, граф неуронске мреже, \textit{COGMEN}.

\newpage
\begin{english}
\begin{center}
PREDICTIVE SELF-SUPERVISED LEARNING OF MULTIMODAL REPRESENTATIONS FOR EMOTION RECOGNITION IN CONVERSATION\par\vspace{1cm}
{\bfseries ABSTRACT}
\end{center}
\vspace{0.5cm}

Emotion recognition in conversation is the task of determining the emotion of each utterance in a dialogue, where the emotion depends on what was said, how it was said, the speaker's facial expression and the preceding course of the conversation. The COGMEN model addresses this problem with a graph neural network over the conversation, in which a context extractor based on a transformer encoder produces utterance representations from precomputed textual, audio and visual features. However, this encoder is trained exclusively on emotion labels, while emotion recognition datasets are small.

This thesis proposes self-supervised pre-training of the COGMEN context extractor following the Joint Embedding Predictive Architecture (JEPA). During pre-training, individual modalities of utterances or future utterances are masked, and the model predicts, from the visible part of the conversation, the representations of the masked parts produced by a target encoder whose weights are updated as an exponential moving average. After pre-training, the encoder is used as the context extractor of COGMEN, which is then trained on emotion labels.

Three hypotheses are formulated: that pre-training leads to better utterance representations and better separation of similar emotions, that modality masking makes the model more robust to missing modalities, and that temporal masking enables prediction of the emotions of future utterances. The hypotheses will be evaluated on the IEMOCAP and CMU-MOSEI datasets using weighted and macro F1 scores, by comparison with the original COGMEN model and with generative pre-training as a control experiment. In addition, an analysis of how the model makes decisions is planned, based on graph transformer attention coefficients, relation-type ablation and the GNNExplainer method, together with a fallback approach in which the model combines pre-trained and original representations through a gating mechanism.

\vspace{0.5cm}
\noindent\textbf{Keywords:} emotion recognition in conversation, multimodal learning, self-supervised learning, JEPA, graph neural networks, COGMEN.
\end{english}

\newpage
\noindent{\large СПИСАК КОРИШЋЕНИХ СКРАЋЕНИЦА И ОЗНАКА}\par
\vspace{0.8cm}
\noindent СКРАЋЕНИЦЕ\par\medskip
{\raggedright
\noindent A-JEPA -- \textit{JEPA} модел за звук (\textbf{A}udio-JEPA)\par\smallskip
\noindent AdamW -- \textit{Adam} оптимизатор са раздвојеним \textit{weight decay}-ом (\textbf{Adam} with decoupled \textbf{W}eight decay)\par\smallskip
\noindent BERT -- двосмерне енкодерске репрезентације из трансформера (\textbf{B}idirectional \textbf{E}ncoder \textbf{R}epresentations from \textbf{T}ransformers)\par\smallskip
\noindent BYOL -- метод самонадгледаног учења (\textbf{B}ootstrap \textbf{Y}our \textbf{O}wn \textbf{L}atent)\par\smallskip
\noindent CMU-MOSEI -- скуп података за анализу сентимента и емоција (\textbf{CMU} \textbf{M}ultimodal \textbf{O}pinion \textbf{S}entiment and \textbf{E}motion \textbf{I}ntensity)\par\smallskip
\noindent COGMEN -- граф неуронска мрежа за мултимодално препознавање емоција (\textbf{CO}ntextualized \textbf{G}NN based \textbf{M}ultimodal \textbf{E}motion recognitio\textbf{N})\par\smallskip
\noindent E5M2 -- \textit{float8} формат са пет бита експонента и два бита мантисе (5-bit \textbf{E}xponent, 2-bit \textbf{M}antissa)\par\smallskip
\noindent EMA -- експоненцијални покретни просек (\textbf{E}xponential \textbf{M}oving \textbf{A}verage)\par\smallskip
\noindent ERC -- препознавање емоција у конверзацији (\textbf{E}motion \textbf{R}ecognition in \textbf{C}onversation)\par\smallskip
\noindent FP8 -- 8-битни формат бројева са покретним зарезом (\textbf{8}-bit \textbf{F}loating \textbf{P}oint)\par\smallskip
\noindent FPGA -- програмабилно поље логичких кола (\textbf{F}ield-\textbf{P}rogrammable \textbf{G}ate \textbf{A}rray)\par\smallskip
\noindent GAT -- граф мрежа са механизмом пажње (\textbf{G}raph \textbf{At}tention Network)\par\smallskip
\noindent GCN -- граф конволуциона неуронска мрежа (\textbf{G}raph \textbf{C}onvolutional \textbf{N}etwork)\par\smallskip
\noindent GCNet -- мрежа за допуну графа (\textbf{G}raph \textbf{C}ompletion \textbf{Net}work)\par\smallskip
\noindent GELU -- Гаусова линеарна јединица грешке (\textbf{G}aussian \textbf{E}rror \textbf{L}inear \textbf{U}nit)\par\smallskip
\noindent GNN -- граф неуронска мрежа (\textbf{G}raph \textbf{N}eural \textbf{N}etwork)\par\smallskip
\noindent GPT -- генеративни претренирани трансформер (\textbf{G}enerative \textbf{P}re-trained \textbf{T}ransformer)\par\smallskip
\noindent I-JEPA -- \textit{JEPA} модел за слике (\textbf{I}mage-JEPA)\par\smallskip
\noindent IEMOCAP -- скуп података снимака дијалога (\textbf{I}nteractive \textbf{E}motional Dyadic \textbf{Mo}tion \textbf{Cap}ture)\par\smallskip
\noindent InfoNCE -- контрастивна функција губитка (\textbf{Info}rmation \textbf{N}oise-\textbf{C}ontrastive \textbf{E}stimation)\par\smallskip
\noindent JEPA -- архитектура за предвиђање у заједничком простору репрезентација (\textbf{J}oint \textbf{E}mbedding \textbf{P}redictive \textbf{A}rchitecture)\par\smallskip
\noindent LLM -- велики језички модел (\textbf{L}arge \textbf{L}anguage \textbf{M}odel)\par\smallskip
\noindent LSTM -- мрежа са дугом краткорочном меморијом (\textbf{L}ong \textbf{S}hort-\textbf{T}erm \textbf{M}emory)\par\smallskip
\noindent MAE -- аутоенкодер са маскирањем (\textbf{M}asked \textbf{A}uto\textbf{e}ncoder)\par\smallskip
\noindent MELD -- мултимодални скуп података дијалога (\textbf{M}ultimodal \textbf{E}motion\textbf{L}ines \textbf{D}ataset)\par\smallskip
\noindent MMIN -- мрежа за замишљање недостајућег модалитета (\textbf{M}issing \textbf{M}odality \textbf{I}magination \textbf{N}etwork)\par\smallskip
\noindent MSE -- средња квадратна грешка (\textbf{M}ean \textbf{S}quared \textbf{E}rror)\par\smallskip
\noindent PAD -- тродимензионални модел емоција (\textbf{P}leasure-\textbf{A}rousal-\textbf{D}ominance)\par\smallskip
\noindent ReLU -- исправљена линеарна јединица (\textbf{Re}ctified \textbf{L}inear \textbf{U}nit)\par\smallskip
\noindent RGCN -- релациона граф конволуциона мрежа (\textbf{R}elational \textbf{G}raph \textbf{C}onvolutional \textbf{N}etwork)\par\smallskip
\noindent RNN -- рекурентна неуронска мрежа (\textbf{R}ecurrent \textbf{N}eural \textbf{N}etwork)\par\smallskip
\noindent sBERT -- модел за репрезентације реченица заснован на \textit{BERT}-у (\textbf{S}entence-\textbf{BERT})\par\smallskip
\noindent Seq2Seq -- модел секвенца у секвенцу (\textbf{Seq}uence-\textbf{to}-\textbf{Seq}uence)\par\smallskip
\noindent SimCLR -- метод контрастивног учења (\textbf{Sim}ple framework for \textbf{C}ontrastive \textbf{L}earning of visual \textbf{R}epresentations)\par\smallskip
\noindent SSL -- самонадгледано учење (\textbf{S}elf-\textbf{S}upervised \textbf{L}earning)\par\smallskip
\noindent TS-JEPA -- \textit{JEPA} модел за временске серије (\textbf{T}ime \textbf{S}eries-JEPA)\par\smallskip
\noindent V-JEPA -- \textit{JEPA} модел за видео (\textbf{V}ideo-JEPA)\par\smallskip}

\newpage
\noindent ОЗНАКЕ\par\medskip
{\raggedright
\noindent $C$ -- број класа\par\smallskip
\noindent $P_c$, $R_c$ -- прецизност и одзив класе $c$\par\smallskip
\noindent $F1_c$ -- F1 мера класе $c$\par\smallskip
\noindent $F1_w$ -- пондерисана F1 мера\par\smallskip
\noindent $F1_{\mathrm{macro}}$ -- макро F1 мера\par\smallskip
\noindent $\eta$ -- стопа учења\par\smallskip
\noindent $\sigma$ -- сигмоидна функција\par\smallskip
\noindent $\odot$ -- множење елемент по елемент\par\smallskip
\noindent $Q$, $K$, $V$ -- матрице упита (енгл. \textit{Query}), кључева (енгл. \textit{Key}) и вредности (енгл. \textit{Value}) у механизму пажње\par\smallskip
\noindent $W_Q$, $W_K$, $W_V$ -- матрице тежина за упите, кључеве и вредности\par\smallskip
\noindent $d_k$ -- димензија вектора упита и кључева\par\smallskip
\noindent $G = (V, E)$ -- граф са скупом чворова $V$ и скупом грана $E$\par\smallskip
\noindent $\mathcal{N}(u)$ -- скуп суседа чвора $u$\par\smallskip
\noindent $h_u^{(k)}$ -- репрезентација чвора $u$ након $k$ итерација размене порука\par\smallskip
\noindent $u_i^{(t)}$, $u_i^{(a)}$, $u_i^{(v)}$ -- текстуална, аудио и видео обележја изговора $i$\par\smallskip
\noindent $x_c$ -- маскирани улаз, односно контекст\par\smallskip
\noindent $f_\theta$ -- енкодер контекста са параметрима $\theta$\par\smallskip
\noindent $f_{\bar\theta}$ -- циљни енкодер са параметрима $\bar\theta$\par\smallskip
\noindent $g_\phi$ -- предиктор са параметрима $\phi$\par\smallskip
\noindent $h_c$ -- репрезентација контекста\par\smallskip
\noindent $h_t$, $\hat{h}_t$ -- циљне и предвиђене репрезентације маскираних делова\par\smallskip
\noindent $m$ -- коефицијент експоненцијалног покретног просека\par\smallskip
\noindent $\tau$ -- параметар температуре у контрастивном губитку\par\smallskip
\noindent $r$ -- тип релације у релационој граф неуронској мрежи\par\smallskip
\noindent $g_i$ -- вредност \textit{gate}-а за изговор $i$\par\smallskip}
```
