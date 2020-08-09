---
title: Python 자소 분리 현상 해결하기  
date: 2020-08-09 16:10:00 +0900
categories: [NLP, Preprocessing]
tags: [python, korean, preprocessing] 
---

Mac OS 에서 만든 파일을 window에서 확인할 때 자소가 분리되어 보이는 경우가 있다. 

Mac OS 는 한글 음절을 초성, 중성, 종성으로 나누는 `NFD` 방식으로 저장하기 때문인데, 음절 그대로 저장하기 위해서는 `NFC` 방식을 사용해야 한다. 

예를 들어, `가` 이라는 문자는 `NFC` 에서는 `U+AC00(가)` 한 글자로 저장하는데, `NFD` 에서는 `U+1100(초성ㄱ)`, `U+1161(중성ㅏ)` 두 글자로 저장한다. 

한글 처리를 위해 만들어진 패키지는 아니지만, Python 에서는 NFD-NFC 변환 함수가 포함된 `unicodedata` 라는 기본 패키지를 제공한다.


```python
import unicodedata 

nfc_sentence = '그는 괜찮은 척하려고 애쓰는 것 같았다.'

# NFC -> NFD 변환 
nfd_sentence = unicodedata.normalize('NFD', nfc_sentence)
print(len(nfd_sentence), nfd_sentence)

# NFD -> NFC 변환 
nfc_sentence = unicodedata.normalize('NFC', nfd_sentence)
print(len(nfc_sentence), nfc_sentence)
```
