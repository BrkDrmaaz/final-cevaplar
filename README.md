# final-cevaplar

Project Euler

Problem 5

function smallestMult(n) {
    let inc = 2;
    let step = 2;
    let smallestNum = 2;
    while (smallestNum <= Number.MAX_SAFE_INTEGER) {
      for (let i = 2; i <= n; i++) {
        const divisible = smallestNum % i === 0;
        if (!divisible) {
          break;
        }
        if (i === inc) {
          step = smallestNum;
          inc++;
        }
        if (i === n) {
          return smallestNum;
        }
      }
      smallestNum += step;
    }

Problem 35

function findPrimes(range) {
    var numbers = [1];
    var prime = 2;
    var primesArr = [2]
    while(prime < range) {
        for(var i = 1; i <= range && prime * i <= range ; ++i) {
            numbers[prime * i - 1] = prime * i;
        }
        while(numbers[prime-1] !== undefined) {
            ++prime;
        }
        primesArr.push(prime);
    }
    primesArr.pop();
    return primesArr;
}
function findCircularPrimes(range) {
    var primes = findPrimes(range);
    var circularPrimes = [];
    for(var i = 0; i < primes.length; ++i) {
        var numArr = primes[i].toString().split('');
        var truefalse = true;
        for (var j = 0; j < numArr.length; ++j) {
            numArr.push(numArr.shift());
            if (primes.indexOf(Number(numArr.join(''))) === -1) {
                truefalse = false;
                break;
            }
        }
        if(truefalse) {
            circularPrimes.push(primes[i]);
        }
    }
    return circularPrimes;
}
var then = Date.now();
var primes = findCircularPrimes(100000).length
alert(primes);

Problem 85

function a(m) {
    return m * (m + 1) / 2;
}

function main() {
    var d = 2000000;
    var m = 1;
    var m0 = 0;
    var n0 = 0;
    for (;;) {
        var n = Math.ceil(Math.sqrt((2000000 / a(m)) * 2));
        if (m > n) break;
        for (;;) {
            var v = a(m) * a(n);
            var e = Math.abs(v - 2000000);
            if (d > e) {
                d = e;
                m0 = m;
                n0 = n;
            }
            if (v < 2000000 - d) {
                break;
            }
            n = n - 1;
        }
        m = m + 1;
    }
    return m0 * n0;
}

console.log('Cevaps: ' + main());
alert(main());


Problem 15

var numRoutes = [];

var getNumRoutes = function (sizeX, sizeY) {
    numRoutes[sizeX] = numRoutes[sizeX] || []

    if (numRoutes[sizeX][sizeY]) {
        return numRoutes[sizeX][sizeY];
    }
    if (sizeX == 0 || sizeY == 0) return 1;

    //Consider moving to the right
    var routes = getNumRoutes(sizeX-1, sizeY);
    routes += getNumRoutes(sizeX, sizeY - 1);
    
    numRoutes[sizeX][sizeY] = routes;

    return routes;

};

console.log(getNumRoutes(2, 2));
console.log(getNumRoutes(20, 20));

alert(getNumRoutes(20, 20));

Problem 25

var bigNumber = {};

/**
 * 
 *
 * @param digits1 
 * @param digits2 
 * @return 
 */
bigNumber.digitArrayAdd = function(digits1, digits2) {
    var sumDigits = [];
    var length = digits1.length > digits2.length ? digits1.length : digits2.length;
    
    for(var i = 0; i < length; i++){
        sumDigits[i] = (digits1[i] || 0) + (digits2[i] || 0) + (sumDigits[i] || 0);
        bigNumber.rebalanceDigitArray(sumDigits, i);
    }
    
    return sumDigits;
}; 
/**
 * 
 *
 * @param digits 
 * @param index 
 */
bigNumber.rebalanceDigitArray = function(digits, index) {
    var digit = digits[index];
    while (digit > 9) {
        digits[index] = digit % 10;

        index++;
        digits[index] = digit = (digits[index] || 0) + ((digit - digit % 10) / 10);
    }
}; 
var getFirstFibTermNumberWithDigits = function(n) {
    if (n <= 1) {
        return 1;
    }

    var previous = [1];
    var current = [1];
    var counter = 2;

    while (current.length < n) {
        var temp = current;
        current = bigNumber.digitArrayAdd(previous, current);
        previous = temp;
        counter++;
    }
    console.log('Fib Number is: ' + current.reverse().toString().replace(/,/g, ''));

    return counter;
};

console.log(getFirstFibTermNumberWithDigits(3));
console.log(getFirstFibTermNumberWithDigits(1000));


alert(getFirstFibTermNumberWithDigits(1000))

Leetcode

Problem 5

/**
 * @param {string} s
 * @return {string}
 */


var longestPalindrome = function(s) {
    if(s === null || s.length === 0){
        return "";
    }    
    
    var result = "";
    var len = 2*s.length - 1;
    var left, right;
    
    for(var i = 0; i < len; i++){
        left = right = parseInt(i/2);
        if(i%2 === 1){
            right++;
        }
        
        var str = expandFromCenterAndCheckForPalindrome(s,left,right);
        
        if(str.length > result.length){
            result = str;
        }
    }
    return result;
};
var longestPalindrome = function(s) {
    if(s === null || s.length === 0){
        return "";
    }    
    
    var result = "";
    var len = s.length;
    var left, right;
    
    for(var i = 0; i < len; i++){
        left = right = i;

        var str = expandFromCenterAndCheckForPalindrome(s,left,right);
        if(str.length > result.length){
            result = str;
        }
        var str = expandFromCenterAndCheckForPalindrome(s,left,right + 1);
        if(str.length > result.length){
            result = str;
        }
    }
    return result;
};


var expandFromCenterAndCheckForPalindrome = function(s, left, right){
    while(left >= 0 && right < s.length && s[left] === s[right]){
        left--;
        right++;
    }
    
    return s.substring(left+1, right);
}

alert(longestPalindrome( 'babad' ));

Problem 35

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchInsert = function(nums, target) {
    var left = 0;
    var right = nums.length - 1;
    
    while(left <= right){
        var mid = parseInt((left + right)/2);
        
        var val = nums[mid];
        
        if(val === target){
            return mid;
        } else if(val > target){
            right = mid - 1;
        } else {
            left = mid + 1;
        }
    }
    
    if(nums[left] < target){
        return left + 1;
    } else {
        return left;
    }
};

alert(searchInsert([1,3,5,6], 5));

Problem 350

/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
var intersect = function(nums1, nums2) {
    var hash = {};
    var arr1, arr2;

    if(nums1.length > nums2.length) {
        arr1 = nums2;
        arr2 = nums1;
    } else {
        arr1 = nums1;
        arr2 = nums2;
    }

    var count = arr1.length;
    var result = [];
    
    for(var i = 0; i < arr1.length; i++) {
        hash[arr1[i]] = hash[arr1[i]] || 0;
        hash[arr1[i]]++;
    }
    
    for(i = 0; i < arr2.length && count !== 0; i++) {
        if(hash[arr2[i]] > 0) {
            hash[arr2[i]]--;
            count--;
            result.push(arr2[i]);
        }
    }
    
    return result;
};

alert(intersect(nums1 = [1,2,2,1] , nums2 = [2,2] ))

Problem 865

  @param {TreeNode} root
  @return {TreeNode}
 
const subtreeWithAllDeepest = function(root) {
    return dfs(root).node;
  };
  
  function dfs(node) {
    if (node == null) return new result(null, 0);
    const l = dfs(node.left);
    const r = dfs(node.right);
    if (l.dist > r.dist) return new result(l.node, l.dist + 1);
    if (l.dist < r.dist) return new result(r.node, r.dist + 1);
    return new result(node, l.dist + 1);
  }
  
  function result(node, dist) {
    this.node = node;
    this.dist = dist;
  }

Problem 895

const FreqStack = function() {
    this.stack = Array.from({length: 10001}, () => [])
    this.maxf = 0
    this.freq = {}
  };
  

 @param {number} x
 @return {void}

  FreqStack.prototype.push = function(x) {
    if(!this.freq[x]) this.freq[x] = 0
    this.freq[x]++
    if(this.freq[x] > this.maxf) this.maxf = this.freq[x]
    this.stack[this.freq[x]].push(x)
  };
  

 @return {number}
 
  FreqStack.prototype.pop = function() {
    let res = this.stack[this.maxf].pop()
    if(this.stack[this.maxf].length === 0) this.maxf--
    this.freq[res]--
    return res
  };


