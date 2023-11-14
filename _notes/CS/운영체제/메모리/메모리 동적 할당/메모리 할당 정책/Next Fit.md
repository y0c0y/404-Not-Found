이전 탐색이 종료된 시점부터 탐색함.

 ! next-fit은 pointp, 즉 탐색 포인터를 변경해줘야 하기 때문에 find_fit 뿐만 아니라 다른 함수의 코드도 수정해야함.

```C
static void *next_fit(size_t asize)
{
    void *bp;
    void *old_pointp = pointp;
    for (bp = pointp; GET_SIZE(HDRP(bp)); bp = NEXT_BLKP(bp))
    {
        if (!GET_ALLOC(HDRP(bp)) && GET_SIZE(HDRP(bp)) >= asize)
        {
            pointp = NEXT_BLKP(bp);
            return bp;
        }
    }
    for (bp = heap_listp; bp < old_pointp; bp = NEXT_BLKP(bp))
    {
        if ((!GET_ALLOC(HDRP(bp))) && GET_SIZE(HDRP(bp)) >= asize)
        {
            pointp = NEXT_BLKP(bp);
            return bp;
        }
    }
    return NULL;
}
```

이전 탐색의 종료지점 부터, 크기가 0이 아닐 동안, 즉 에필로그 헤더가 나오기 전까지, 다음 블록으로 이동하면서 원하는 크기 이상의 가용블록을 선택한다.

이전 탐색의 종료지점부터 찾았는데 사용할 수 있는 블록이 없다면, 다시 앞에서부터 이전 탐색의 종료지점 전까지 이동하면서 선택한다.   
탐색 포인터를 현재 선택된 블록 다음으로 설정한다.