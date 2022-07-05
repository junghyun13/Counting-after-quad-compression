# Counting-after-quad-compression
# python
# Counting after quad compression I have a two-dimensional array of integers arr of size 2n x 2n of 0s and 1s. You want to compress this arr in the same way as a quad tree. Define the specific area you want to compress as S. If all numbers in S are the same, then we compress S to one. Otherwise, split S into exactly 4 uniform square regions (see the input/output example), and try to compress each square region in the same way. 
# 0과 1로 이루어진 2n x 2n 크기의 2차원 정수 배열 arr이 있습니다. 당신은 이 arr을 쿼드 트리와 같은 방식으로 압축하고자 합니다. 당신이 압축하고자 하는 특정 영역을 S라고 정의합니다. 만약 S 내부에 있는 모든 수가 같은 값이라면, S를 해당 수 하나로 압축시킵니다. 그렇지 않다면, S를 정확히 4개의 균일한 정사각형 영역으로 쪼갠 뒤, 각 정사각형 영역에 대해 같은 방식의 압축을 시도합니다.
# not use after quad compression/ test1 is [[1,1,0,0],[1,0,0,0],[1,0,0,1],[1,1,1,1]] test2 is [[1,1,1,1,1,1,1,1],[0,1,1,1,1,1,1,1],[0,0,0,0,1,1,1,1],[0,1,0,0,1,1,1,1],[0,0,0,0,0,0,1,1],[0,0,0,0,0,0,0,1],[0,0,0,0,1,0,0,1],[0,0,0,0,1,1,1,1]] but not correct test2
def solution(arr):
    answer = [0]*2
    cnt=0
    count=0
    for i in range(0,len(arr)):
        cnt+=1
        for j in range(0,len(arr)):
            if arr[i][j]==1:
                count+=1
    answer=list((cnt,count))
    return answer
arr=[[1,1,0,0],[1,0,0,0],[1,0,0,1],[1,1,1,1]]
a=solution(arr)
print(a)
#result--> [4, 9]
# this code is correct for test1 and test2
def solution(arr):
    result=[0,0]
    length=len(arr)
    def compression(a,b,l):
        start=arr[a][b]
        for i in range(a,a+l):
            for j in range(b,b+l):
                if arr[i][j]!=start: #이부분이 1과 0을 구분해준다!
                    l=l//2
                    compression(a,b,l)
                    compression(a,b+l,l)
                    compression(a+l,b,l)
                    compression(a+l,b+l,l)
                    return       
        result[start]+=1       
    compression(0,0,length)  
    return (result)
arr=[[1,1,1,1,1,1,1,1],[0,1,1,1,1,1,1,1],[0,0,0,0,1,1,1,1],[0,1,0,0,1,1,1,1],[0,0,0,0,0,0,1,1],[0,0,0,0,0,0,0,1],[0,0,0,0,1,0,0,1],[0,0,0,0,1,1,1,1]]
a=solution(arr)
print(a)
#result--> [10,15]
