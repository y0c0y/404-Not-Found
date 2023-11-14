처음부터 탐색하고 크기가 맞는 첫 가용 블록을 선택함.

힙의 시작 부터, 크기가 >0일때동안, 즉 에필로그 헤더가 나오기 전까지 다음 블록으로 이동하면서 원하는 크기 이상의 가용 블록을 찾는다. 가장 먼저 찾은 (원하는 크기 이상의 가용)블록을 선택함. 

```C
static void *first_fit(size_t asize)
{
    void *bp;
    for (bp = heap_listp; GET_SIZE(HDRP(bp)) > 0; bp = NEXT_BLKP(bp))
    {
        if (GET_SIZE(HDRP(bp)) >= asize && (!GET_ALLOC(HDRP(bp))))
        {
            return bp;
        }
    }
    return NULL;
}
```