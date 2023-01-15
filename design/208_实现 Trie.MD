## 208.实现 Trie
题目大意：
Trie（发音类似 "try"）或者说 前缀树 是一种树形数据结构，用于高效地存储和检索字符串数据集中的键。这一数据结构有相当多的应用情景，例如自动补完和拼写检查。    
请你实现 Trie 类：  
Trie() 初始化前缀树对象。  
void insert(String word) 向前缀树中插入字符串 word 。  
boolean search(String word) 如果字符串 word 在前缀树中，返回 true（即，在检索之前已经插入）；否则，返回 false 。  
boolean startsWith(String prefix) 如果之前已经插入的字符串 word 的前缀之一为 prefix ，返回 true ；否则，返回 false 。  

## 代码
```go
type Trie struct {
    children [26]*Trie
    isEnd bool
}


func Constructor() Trie {
    return Trie{}
}


func (this *Trie) Insert(word string)  {
    for _, w := range word {
        w -= 'a'
        if this.children[w] == nil {
            this.children[w] = &Trie{}
        }
        this = this.children[w]
    }
    this.isEnd = true
}


func (this *Trie) Search(word string) bool {
    node := this.searchPrefix(word)
    return node != nil && node.isEnd
}


func (this *Trie) StartsWith(prefix string) bool {
    return this.searchPrefix(prefix) != nil
}

func (this *Trie) searchPrefix(prefix string) *Trie {
      for _, w := range prefix {
        w -= 'a'
        if this.children[w] == nil {
            return nil
        }
        this = this.children[w]
    }
    return this  
}


/**
 * Your Trie object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Insert(word);
 * param_2 := obj.Search(word);
 * param_3 := obj.StartsWith(prefix);
 */
```

## 复杂度
时间复杂度 O(n): n 为插入/查询的字符串的长度  
空间复杂度 O(k*n): k 是字符集大小，即 26；n 为 Tire 节点的数量  