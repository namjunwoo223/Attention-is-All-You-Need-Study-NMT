# Attention-is-All-You-Need-Study-NMT
AiHub데이터로 Attention 공부 및 NMT(기계 번역) 모델 제작 

# 설명
나동빈님의 code practice를 기초로 Transformer의 구조를 이해하고 적용해보는 repository입니다.
예시에서는 영어와 독일어를 번역하는 모델로 나왔으나, 커스텀 데이터로 적용을 해 보는게 이해에 가장 빠를 것 이라 생각하여
Aihub 데이터 중 한국어-일본어 말 뭉치 데이터를 이용하여 NMT모델을 구현해봤습니다.
일본어 Tokenizer는 spacy에 있는 `ja_core_news_md`를 이용하여 tokenize를 진행하였고 한국어의 경우 konlpy의 `Otk`를 이용하여 토크나이징을 진행하였습니다.

# Data
한국어-일본어 말 뭉치 : https://aihub.or.kr/aidata/30723

# 문제점
기존 나동빈님의 코드에는 torchtext의 0.6.0의 버전에서 지원하는 Filed를 사용하는 dataset방식을 차용하셨습니다만, 
이 경우 Tokenizer가 spacy로 만들어야 제대로 된 Tokenizing이 되는 것을 확인하였으며, 아쉽게도 spacy는 일본어 Tokenizer는 지원했지만 한국어 Tokenizer는 지원하지 않았습니다.
따라서, 직접 데이터 선언 부분을 torchtext에서 지원하는 방식과 비슷하게 Vocab dictionary, dataset 코드를 새로 제작하였습니다.
다만, 개인적으로 아쉬운 점은 데이터량이 많아 질 수록 Vocab크기가 커지며 학습속도와 처리속도가 느렸습니다.
또한, 어느정도 번역이 동작하긴 하지만, vocab의 의존이 높고 말이 안되게 출력되는 경우도 확인하였습니다.
나중에 좀 더 다듬을 수 있는 방법을 고민해 보고 싶습니다.

# 추가
기존 코드에서 vocab구축에 있어서 시간이 많이 드는 단점을 직렬화를 통해 해결 할 수 있을 것 같습니다.
또한 Okt랑 mecab의 처리속도가 많은 차이가있습니다.

실제로 진행을 해본 결과로 모든 데이터의 형태소분리를 Okt는 5시간이 소요됬지만 mecab의 경우 40분이 소요되었습니다
      
또한, 학습데이터의 개수가 많아짐에 따라서 학습속도가 느려지고 Vram의 요구가 많아지는데 저 같은 경우 이것의 해결법으로 TPU로 돌려보는 방향으로 보고있습니다.

코드를 계속 테스트중이며 잘 되면 추후 공유하겠습니다.

# 공부 방식
저 같은 경우 코드 내 함수 였던 Transformer -> Encoder -> Decoder 순으로 코드와 논문을 번갈아가며 보면서 
코드 작성 방법을 고민하면서 학습하였고 모르는 것들이 있다면 나동빈님의 유튜브와 논문 리뷰등을 활용하면서 공부를 진행하였습니다.
각자 편한 방식으로 공부하시면 좋을 것 같습니다.

# Reference
나동빈님 Attention is All you Need 논문 뿌수는 유튜브 : https://www.youtube.com/watch?v=AA621UofTUA

나동빈님 Attention is All you Need Code Practice : https://github.com/ndb796/Deep-Learning-Paper-Review-and-Practice/blob/master/code_practices/Attention_is_All_You_Need_Tutorial_(German_English).ipynb

Attention is all you Need : https://arxiv.org/pdf/1706.03762.pdf

소중한 데이터와 자료를 제공 해 주신 것에 대해 감사의 말씀 전합니다.
