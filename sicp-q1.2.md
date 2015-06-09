## 1.2.1

(define (factorial n)
  (define (iter product counter)
    (if (> counter n)
      product
      (iter (* counter product)
            (+ counter 1))))
  (iter 1 1)
  )

問題1.9

(define (+ a b)
  (if (= a 0)
    b
    (inc (+ (dec a) b))))

(+ 4 5)
(inc (+ (dec 4) 5)) => (inc (+ 3 5))
(inc (inc (+ 2 5)))
(inc (inc (inc (+ 1 5))))
(inc (inc (inc (inc (+ 0 5)))))
(inc (inc (inc (inc 5))))
(inc (inc (inc 6)))
(inc (inc 7))
(inc 8)
9

(define (+ a b)
  (if (= a 0)
    b
    (+ (dec a) (inc b))))

(+ 4 5)
(+ (dec 4) (inc 5))
(+ 3 6)
(+ (dec 3) (inc 6))
(+ (dec 2) (inc 7))
(+ (dec 1) (inc 8))
(+ (dec 0) (inc 9))
9

上は再帰的プロセス、下は反復的プロセス

問題1.10

(define (A x y)
  (cond ((= y 0) 0)
        ((= x 0) (* 2 y))
        ((= y 1) 2)
        (else (A (- x 1)
                (A x (- y 1))))))

gosh> (A 1 10)
1024

gosh> (A 2 4)
65536

gosh> (A 3 3)
65536

正の整数nに対する以下の手続きの数学的定義。
(define (f n) (A 0 n))
(f n)は2nを計算する。

(define (g n) (A 1 n))
xが1なので、(A 0 (A 1 (- y 1)))
yが3の場合で展開してみると
(g 3)
(A 1 3)
(A 0 (A 1 2))
(A 0 (A 0 (A 1 1)))
(A 0 (A 0 2))
(A 0 4)
8

yが1になるまで展開を続け、(A 0 1)が2となったあと、収束をしていく。
2のy乗を計算する。ただし、y=0の場合は0を返す。

(define (h n) (A 2 n))
xが2なので(A 1 (A 2 (- n 1))) の手続きとなる。
(A 1 n)は2のn乗であることはわかっている。
(A 2 (- n 1))は再帰的に(A 1 (A 2 (- n 2))) へと展開される。これはnが1になるまで続く。
(h 4)の場合を展開してみる。

(h 4)
(A 2 4)
(A 1 (A 2 3))
(A 1 (A 1 (A 2 2)))
(A 1 (A 1 (A 1 (A 2 1))))
(A 1 (A 1 (A 1 2)))
(A 1 (A 1 4))
(A 1 16)
65536

2の(2の(n-1)乗)乗
2 => 2乗
3 => 4乗
4 => 16乗
5 => 65536乗

(h 5)
(A 2 5)
(A 1 (A 2 4))
(A 1 (A 1 (A 2 3)))
(A 1 (A 1 (A 1 (A 2 2))))
(A 1 (A 1 (A 1 (A 1 (A 2 1)))))
(A 1 (A 1 (A 1 (A 1 2))))
(A 1 (A 1 (A 1 4)))
(A 1 (A 1 16))
(A 1 65536)


(A 1 (A 2 4))
(A 1 (A 1 (A 2 2)))
(A 1 (A 1 (A 1 (A 2 1))))
(A 1 (A 1 (A 1 2)))
(A 1 (A 1 4))
(A 1 16)

2の(2の(2の(2の1乗)乗)乗）のカッコがn続くようなもの。

## 1.2.2

(define (fib n)
  (cond ((= n 0) 0)
        ((= n 1) 1)
        (else (+ (fib (- n 1))
                  (fib (- n 2))))))

両替

(define (count-change amount)
  (cc amount 5))

(define (cc amount kinds-of-coins)
  (cond ((= amount 0) 1)
        ((or (< amount 0) (= kinds-of-coins 0)) 0)
        (else (+ (cc amount
                    (- kinds-of-coins 1))
                  (cc (- amount
                        (first-denomination kinds-of-coins))
                        kinds-of-coins)))))

(define (first-denomination kinds-of-coins)
  (cond ((= kinds-of-coins 1) 1)
        ((= kinds-of-coins 2) 5)
        ((= kinds-of-coins 3) 10)
        ((= kinds-of-coins 4) 25)
        ((= kinds-of-coins 5) 50)
         ))
