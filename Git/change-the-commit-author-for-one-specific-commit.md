1. Checkout the commit we are trying to modify,  assumed to be 03f482d6
    ```javascript
    git checkout 03f482d6 
    ```

2. Make the author change.
```javascript
    git commit --amend --author "New Author Name <New Author Email>"
```

3. Now we have a new commit with hash assumed to be 42627abe.  
    Checkout the original branch.Replace the old commit with the new one locally.
```javascript
     git replace 03f482d6 42627abe
```
 4. Rewrite all future commits based on the replacement.
```javascript
     git filter-branch -- --all
```
 5. Remove the replacement for cleanliness.
```javascript
     git replace -d 03f482d6
```
 6 Push the new history (only use --force if the below fails, and only after sanity checking with git log and/or git diff).
```javascript
     git push --force-with-lease
```

