# 강화 학습

## OpenAI Gym 환경
### 새로운 환경 생성

다음 코드를 사용해서 새로운 환경을 생성합니다: 

```
import gym
import deeprl_hw1.envs

env = gym.make('Deterministic-4x4-FrozenLake-v0')
```

### 움직임

네 가지 움직임이 있습니다. LEFT, UP, DOWN, RIGHT는 정수로 표현됩니다.
`deep_rl_hw1.envs` 에 이와 관련된 변수들이 선언되어 있습니다. 예를 들면,

```
print(deeprl_hw1.envs.LEFT)
```

는 0을 출력합니다.

### 환경 특성

이 클래스는 다음과 같은 중요한 특성들이 있습니다. 

- `nS` :: 상태의 개수 
- `nA` :: 움직임의 개수
- `P` :: 전이, 보상, 단말

특성 `P` 가 가치 순환법과 정책 순환법을 구현하는 데 가장 중요할 것입니다. 
이 특성은 특정 맵핑 인스턴스에 대한 모델을 가지고 있습니다.
다음과 같이 리스트에 대한 사전에 대한 사전을 형태를 가지고 있습니다.   

```
P[s][a] = [(prob, nextstate, reward, is_terminal), ...]
```

예를 들면, 상태 0에서 LEFT로 움직일 확률을 구하려면 다음과 같은 코드를 쓰면 됩니다. 

```
env.P[0][deeprl_hw1.envs.LEFT]
```

This would return the list: `[(1.0, 0, 0.0, False)]` for the
`Deterministic-4x4-FrozenLake-v0` domain. There is one tuple in the
list, so there is only one possible next state. The next state will be
state 0, according to the second number in the tuple. This will be the
next state 100\% of the time according to the first number in the
tuple. The reward function for this state action pair `R(0,LEFT) = 0`
according to the third number. The final tuple value says that the
next state is not terminal.

##
### 임의의 정책 돌리기

example.py 안에 임의의 정책으로 돌리는 예시가 담겨있습니다. 

#가치 순환법
여러 환경에 대한 최적 정책은 <environment>.py 파일들에 있습니다 
