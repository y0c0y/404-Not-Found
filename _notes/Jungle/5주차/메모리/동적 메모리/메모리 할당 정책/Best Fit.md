모든 가용 블록을 검사해서, 크기에 맞는 가용 블록 중 가장 작은 블록을 찾는다.

```C
static void *best_fit(size_t asize)
{
    void *bp;
    void *best = NULL;
    for (bp = free_listp; GET_ALLOC(HDRP(bp)) != 1; bp = GET_NEXT(bp))
    {
        if (asize <= GET_SIZE(HDRP(bp)))
        {
            if (best == NULL)
            {
                best = bp;
            }
            else if (GET_SIZE(HDRP(bp)) <= GET_SIZE(HDRP(best)))
            {
                best = bp;
            }
        }
    }
    if (best != NULL)
    {
        return best;
    }
    return NULL;
}
```

가용리스트 시작부터 마지막 블록까지 다음 블록으로 이동하면서 원하는 크기 이상인 블록 중 가장 작은 블록을 찾아서 선택