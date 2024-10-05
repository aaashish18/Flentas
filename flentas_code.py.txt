from collections import Counter

def contains_permutation(pattern, text):
    len_p = len(pattern)
    len_t = len(text)
    
    if len_p > len_t:
        return False

    pattern_count = Counter(pattern)
    #print(pattern_count)
    text_count = Counter(text[:len_p])
    #print(text_count)
    if pattern_count == text_count:
        return True

    for i in range(len_p, len_t):

        text_count[text[i]] += 1
        
        text_count[text[i - len_p]] -= 1
        
        if text_count[text[i - len_p]] == 0:
            del text_count[text[i - len_p]]
        
        if pattern_count == text_count:
            return True

    return False

def main():
    T = int(input())
    results = []
    for _ in range(T):
        pattern = input().strip()
        text = input().strip()
        
        if contains_permutation(pattern, text):
            results.append("YES")
        else:
            results.append("NO")
            
    print("\n".join(results))

if __name__ == "__main__":
    main()
