```php
function removeEmojiChar($str)
{
    $mbLen = mb_strlen($str);

    $strArr = [];
    for ($i = 0; $i < $mbLen; $i++) {
        $mbSubstr = mb_substr($str, $i, 1, 'utf-8');
        if (strlen($mbSubstr) >= 4) {
            continue;
        }
        $strArr[] = $mbSubstr;
    }

    return implode('', $strArr);
}
```



