---
fontsize: 12pt
linestretch: 1
indent: true
header-includes: |
  \usepackage{graphicx}
  \usepackage{float}
  \usepackage{subcaption}
  \usepackage{array}
  \usepackage[a4paper, margin=2.5cm]{geometry}
  \usepackage{indentfirst}
  \setlength{\parindent}{12.7mm}
  \AtBeginDocument{\frenchspacing}
  \makeatletter\renewcommand\paragraph{\@startsection{paragraph}{4}{\z@}{3.25ex \@plus1ex \@minus.2ex}{1.5ex \@plus .2ex}{\normalfont\normalsize\bfseries}}\makeatother
  \renewcommand{\contentsname}{Садржај}

  \usepackage{fontspec}
  \usepackage{polyglossia}
  \setdefaultlanguage{serbian}
  \setotherlanguage{english}

  \setmainfont{Times New Roman}
---

{{include sections/0_front/main.md}}

\newpage

\tableofcontents

\newpage

{{include sections/1_introduction/main.md}}

\newpage

{{include sections/2_emotion_recognition/main.md}}

\newpage

{{include sections/3_basics/main.md}}

\newpage

{{include sections/4_cogmen/main.md}}

\newpage

{{include sections/5_jepa/main.md}}

\newpage

{{include sections/6_proposal/main.md}}

\newpage

{{include sections/7_literature/main.md}}