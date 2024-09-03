# about👩‍💻
### _코다 가족은 기록을 어떻게 하나요?_
SKT Fly AI Challenger 과정 진행 중 수행한 **'기록할, 코다'** 프로젝트입니다. 본 프로젝트는 SKT Fly AI Challenger 5기에서 대상🥇을 수상하였습니다.

> ### **코다(CODA)**
> Children of Deaf Adults의 약자로, 농인 부모의 자녀를 의미합니다.
> 이때 농인은 청각장애인 중 수어를 제1언어로 사용하는 사람을 말합니다.

'기록할, 코다'는 농인 사회와 청인 사회 중간에서 정체성 혼란을 겪는 코다와, 그 가족을 위한 서비스로 코다 가족 내 소통 활성화 및 코다와 농인 부모 간 애착 강화를 통한 코다 정체성 확립을 목표로 하고 있습니다.

본 프로젝트에 대한 전체 코드는 아래 링크를 통해 확인해보실 수 있습니다.

[열정1팀 돌맹구 Let's go](https://github.com/StoneMaenggu)


# 서비스 소개
<img width="900" alt="image" src="https://github.com/user-attachments/assets/bdb91664-1380-4c73-9982-95a6ad8cf2f1">



기록할, 코다는 공유앨범형 서비스로 공유 그룹을 형성하고, 그룹 내에서 동일한 포스팅을 공유합니다.


<img width="900" alt="image" src="https://github.com/user-attachments/assets/4f2a010a-ecc8-434e-bc19-3d9254a6cac7">



이때, 농인 부모의 경우 일반적인 텍스트 기반의 SNS 사용이 어렵습니다. 이들은 수어를 제1언어로 사용하기에 수어와 '글로스(gloss)'라는 조사와 어순이 없는 단어 위주로 소통하기 때문입니다.

따라서 기록할, 코다에서는 농인 부모를 위한 수어 및 글로스 입력, 코다를 위한 텍스트 입력, 그리고 기록에 어려움을 갖는 모두를 위한 음성 입력 등을 통해 접근성을 높였습니다.

<img width="900" alt="image" src="https://github.com/user-attachments/assets/a473d548-1ae9-4788-ad35-c80413bcaaa6">

입력에 따라 스토리가 있는 네컷의 이미지를 생성함으로써 쉽게 서로의 이야기를 공유하도록 하였으며, 그날 그날의 사진 역시 첨부가 가능합니다.



**또한, 전체 서비스를 일관적이고, 효율적인 방식으로 구현하기 위한 AI modular Flow는 다음과 같습니다.**
<img width="900" alt="image" src="https://github.com/user-attachments/assets/fd6e44b5-1a01-4168-9e98-45c458323558">

#### 1. Pose2Gloss
더욱 가벼운 모델을 구성하고 사용자의 privacy 문제를 탈피하기 위해 본 프로젝트에서는 mediapipe를 통한 pose estimation을 수행하고, 그 결과를 이용하여 gloss prediction을 수행하였습니다.

이때 수어에서의 Pose는 시공간적 정보이므로 GCN을 통해 공간적 정보를 반영하고, 이에 대한 1D-CNN을 통해 시간적 정보를 반영하였습니다. 이후 Contrastive Learning을 기반으로 Embedding Encoder를 구성하였고, 이를 통해 새로운 수어, 홈싸인, 각종 제스쳐 등을 추가할 수 있도록 하였습니다.

이는 동일한 pose에 대해 여러 의미를 가지며, 사용자마다 조금씩 다르게 사용하는 수어의 특성을 고려한 모델 구조입니다.

#### 2. Gloss2Text
Gloss Prediction의 결과물을 이미지 생성 모델에 넣기 위해서는 온전한 문장 형태로의 전처리 과정이 필요했습니다. 이 부분에서 LLM을 사용하기 보다는 직접 KoBart 및 KoT5를 기반으로 fine-tuning을 진행하였고 최종적으로 BLEU Score 0.72, METEOR Score 0.76으로 높은 성능을 달성하였습니다.


# 시스템 아키텍쳐
<img width="900" alt="image" src="https://github.com/user-attachments/assets/1967b4c8-9c9a-412e-b6c6-ae886fff6795">





