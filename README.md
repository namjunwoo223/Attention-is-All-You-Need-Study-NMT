# Attention-is-All-You-Need-Study-NMT
AiHub데이터로 Attention 공부 및 NMT 모델 제작 

# 설명
나동빈님의 code practice를 기초로 Transformer의 구조를 이해하고 적용해보는 repository입니다.
예시에서는 영어와 독일어를 번역하는 모델로 나왔으나, 커스텀 데이터로 적용을 해 보는게 이해에 가장 빠를 것 이라 생각하여
Aihub 데이터 중 한국어-일본어 말 뭉치 데이터를 이용하였으며 데이터셋이 바뀜으로 코드를 조금 수정하여 진행하였습니다.
일본어 Tokenizer는 spacy에 있는 `ja_core_news_md`를 이용하여 tokenize를 진행하였고 한국어의 경우 konlpy의 Otk를 이용하여 토크나이징을 진행하였습니다.

# Data
한국어-일본어 말 뭉치 : https://aihub.or.kr/aidata/30723

# 문제점
진행하면서 몇 가지 문제점을 발견하였는데 torchtext를 이용하여 데이터셋을 제작 할 시에 꽤 많은 시간이 소요되는 것을 확인하였습니다.
현재 한국어-일본어 말뭉치에서 주어진 데이터셋의 크기는 train : 1,200,000개  valid : 300,000개 이며 이 모든 것을 처리하는데 수십시간 이상이 걸리는 것을 확인하였습니다. 
따라서 torchtext의 의존성을 없애고 자체적으로 전처리를 진행하고 CustomDataset 클래스를 제작하여 데이터 셋 처리 및 Dataloader를 이용하여 제작하는 것이 속도 면에서 이점이 있어보입니다.

또한, 일본어와 한국어 사전 제작에 있어서 너무 다른 주제로 가게 되면 사전 내에 단어가 없어서 UNK토큰을 잔뜩 뱉는 경우가 있습니다.
이런 경우 데이터를 많이 추가하게되면 해결이 가능 해 보입니다.

# To-Do
- [x] Train 베이스라인 제작
- [ ] Attention is All You Need 이론 및 코드 pdf 정리
- [ ] torchtext를 사용하지 않고 데이터 셋 정의 및 모델 수정


# Reference
나동빈님 Attention is All you Need 논문 뿌수는 유튜브 : https://www.youtube.com/watch?v=AA621UofTUA

나동빈님 Attention is All you Need Code Practice : https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Attention_is_All_You_Need_Tutorial_(German_English).ipynb

소중한 데이터와 자료를 제공 해 주신 것에 대해 감사의 말씀 전합니다.
