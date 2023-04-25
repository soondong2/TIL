# Today I Learned - 2023/04/25 

# 베스트 앨범
- 출처 : https://school.programmers.co.kr/learn/courses/30/lessons/42579
- 난이도 : Level3

## 풀이
```python
def solution(genres, plays):
    answer = []
    
    # hash_map1 = {장르 : [재생 횟수, 고유번호(index)]}
    hash_map1 = {}
    for i, g in enumerate(genres):
        if g in hash_map1:
            hash_map1[g].append([plays[i], i])
        else:
            hash_map1[g] = [[plays[i], i]]
    
    # 장르별 총 재생 횟수
    hash_map2 = {}
    for g in hash_map1.keys():
        total = 0
        for i in range(len(hash_map1[g])):
            total += hash_map1[g][i][0]
        hash_map2[g] = total
    
    # 장르별 총 재생 횟수 정렬
    genres_rank = sorted(hash_map2.items(), key=lambda x:x[1], reverse=True)
    
    # 장르 내에서 많이 재생된 노래 정렬
    for g in genres_rank:
        play_rank = sorted(hash_map1[g[0]], key=lambda x:x[0], reverse=True)[:2]
        for p in play_rank:
            answer.append(p[1])
            
    return answer
```
