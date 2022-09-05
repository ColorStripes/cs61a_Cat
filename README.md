# Cat

## Phase 1

### problem 1

- `paragraphs`: a list of strings         一个字符串

- `select:` ：   a function that returns True for paragraphs that can be selected       一个方法

- `k`: 				  an integer 

- **Solution：**

  ```python
      selected = [paragraph for paragraph in paragraphs if select(paragraph)]
      return selected[k] if k < len(selected) else ''
  ```

  

### problem 2

- You may use the string utility functions in `utils.py`. You can reference the docstrings of the utility functions to see how they are being used.

- `topic`是单词敏感列表，这个`about`函数需要返回一个方法，判断`paragraph`里是否有`topic`的词

  Implement `about`, which takes a list of `topic` words. It returns a **function** which takes a paragraph and returns a boolean indicating whether that paragraph contains any of the words in `topic`.

- `lower`： 转换为小写字母

- `remove_punctuation`： 去除标点符号后的句子

### problem 3

- 两个词必须出现在类型和引用中的相同索引处。两个词的第一个词必须匹配，第二个词也必须匹配，依此类推。

   two words must occur at the same indices in typed and reference—the first words of both must match, the second words of both must match, and so on.

- `split`: 把字符串分割成**list**类型

- `zip`函数，python内置函数，打包为元组的列表，感觉上相当于C语言的 `pair`

### prolbem 4

- `elapsed`：the amount of `elapsed` time in **seconds**.  也就是键入字符花费的时间

- `typed`：键入的字符串

- 以五个字符为基数，作为一个单词，键入的字符数除以5就是打了多少个单词

  instead the number of groups of 5 characters, so that a typing test is not biased by the length of words.

- 计算公式：  （总字符长度 /5） * （60s / 花费的秒数）

  ```python
  len(typed) / 5 * 60 / elapsed
  ```

## Phase 2

### problem 5

- `autocorrect`：需要返回差异最小的`TYPED_WORD`，如果差异大于`limit`，则返回`TYPED_WORD`

  - 如果typed_word在valid_words中，返回typed_word。

    If the `typed_word` is contained inside the `valid_words` list, `autocorrect` returns that word.

  - 用`diff_function`找到`valid_words`中与`typed_word`差异最小的单词。

    `autocorrect` returns the word from `valid_words` that has the lowest difference from the provided `typed_word` based on the `diff_function`.

  - 如果最小差异的单词也大于`limit`，返回`typed_word`，否则返回最小差异的单词

    if the lowest difference between typed_word and any of the valid_words is greater than limit, then typed_word is returned instead.

    - `min(diff_list)`：返回最小的差异单词的差异数

    - `index`： 搜索与（）内容匹配的索引数

- `typed_word`:       a string representing a word that may contain typos.                 包含错误单词的字符串
-  `valid_words`:    a list of strings representing valid words.                                    有效的单词的list
- `diff_function`: a function quantifying the difference between two words.          返回两个单词直接的差异数

### problem 6

- `feline_flips`：返回差异字符的个数

  It returns the minimum number of characters that must be changed in the `start` word in order to transform it into the `goal` word.

  - 如果词的长度不同，将长度差添加到总数中。

    If the strings are not of equal length, the difference in lengths is added to the total.

  - 如果差异数大于`limit`，则应该返回比`limit`大的最小计算量的值。

    If the number of characters that must change is greater than `limit`, then `feline_flips` should return any number larger than `limit` and should minimize the amount of computation needed to do so.

- `start`: a starting word.            要对比的单词

- `goal`: a string representing a desired goal word.          模板单词

- `limit`: a number representing an upper bound on the number of chars that must change.       最大差异限制

### problem 7

- `minimum_mewtations`：返回变为`goal`需要修改的最小操作数

- 这里直接引用教案：

  1. `Add` a letter to `start`.
     - Adding `"k"` to `"itten"` gives us `"kitten"`.
  2. `Remove` a letter from `start`.
     - Removing `"s"` from `"scat"` givs us `"cat"`.
  3. `Substitute` a letter in `start` for another.
     - Substituting `"z"` with `"j"` in `"zaguar"` gives us `"jaguar"`.

  - `limit`给的小于0，或者两个字符串都是空 直接返回0
  - 其中一个字符串是空，返回两字符串的长度差值
  - 两个字符相等返回下一个字符开始的数组
  - 比较三种操作的最小值，每操作一次操作次数+1

### Extension: final diff

- 待添加

## Phase 3

### problem8

- `upload`: 下载多人游戏进度的函数

   a function used to upload progress to the multiplayer server. 

- 这个函数只是返回每个id号的游戏进度，进度会根据键入准确的单词计算（正确单词数/总单词数）

   return the progress of the player with `user_id`.

- 测试答案有两行：（格式如下）

    ID: 2 Progress: 0.6
    0.6

### problem 9

- `time_per_word`：根据**时间戳**返回，键入每个单词的时间。

  It returns a `match` with the given information.

- `match`：这个是将单词和玩家id及时间合并成一个元素的方法。合并格式：[words, times]。

  - The `times` are stored as a list of lists of how long it took each player to type every word in `words`. 
  -  Specifically, `times[i][j]` indicates how long it took player `i` to type `words[j]`.

- `words`：a list of words, in the order they are typed.

- `times_per_player`: A list of lists of timestamps including the time the player started typing, followed by the time the player finished typing each word.

- `p`：每一个【】里是每个玩家的时间戳，从起始时间到完成每次字符的时间，后一个数减去前一个数则是完成这个字符花费的时间

- `word_at`：获得索引为word_index的单词

  A selector function that gets the word with index word_index.

- `time`：返回`player_num`在`word_index`处键入单词所需的时间

​		A selector function for the time it took player_num to type the word at word_index

### problem 10

- `fastest_words`：返回各个玩家打字最快的单词列表
- `fastest`：最一开始存储的是玩家编号
- 对比每个单词，是否是当前玩家的最快单词，添加到这个玩家的单词列表里
- 返回单词列表`fastest`

## PlayGame

- **项目演示**：        （呜呜呜，我是笨比，打不快，还老错）

![image-20220905153046059](https://raw.githubusercontent.com/ColorStripes/Typora_Picture/master/picture/image-20220905153046059.png)

## GitHub URL

-  [ColorStripes/cs61a_Cat: cs61a project03 ——Cat (github.com)](https://github.com/ColorStripes/cs61a_Cat)
- First commit by **Xu Xin** at 2022.9.5