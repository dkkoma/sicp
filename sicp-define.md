
### 準備

SICPを読むためにやっておくと便利かもしれないこと

http://qiita.com/da1/items/02f7d2f157c7145d58f2

http://yoshiko.hatenablog.jp/entry/2014/04/10/%E6%95%B0%E5%AD%A6%E3%83%BB%E6%83%85%E5%A0%B1%E7%B3%BB%E3%82%92%E5%B0%82%E6%94%BB%E3%81%97%E3%81%A6%E3%81%AA%E3%81%84Web%E3%82%A8%E3%83%B3%E3%82%B8%E3%83%8B%E3%82%A2%E3%81%8CSICP%E3%82%92%E8%AA%AD


### defineなど

(define (sqrt-iter guess x)
  (if (good-enough? guess x)
    guess
    (sqrt-iter (improve guess x)
      x)))

(define (improve guess x)
  (average guess (/ x guess)))

(define (average x y)
  (/ (+ x y) 2))

(define (abs x)
  (cond ((< x 0) (- x))
        (else x)))

(define (good-enough? guess x)
  (< (abs (- (square guess) x)) 0.001))

(define (square x) (* x x))

(define (sqrt-iter guess x)
  (new-if (good-enough? guess x)
    guess
    (sqrt-iter (improve guess x)
      x)))

*condによる評価のsqrt-iter*

(define (sqrt-iter guess x)
  (cond
    ((good-enough? guess x) guess)
    (else (sqrt-iter (improve guess x) x))
    ))

### tempoary

(define (new-if predicate then-clause else-clause)
  (cond (predicate then-clause)
        (else else-clause)))

(sqrt-iter 1.0 3)

201000000000000

(sqrt-iter 1.0 8000000000000)

### 立方根のよりよい近似値

(define (improve-cubert guess x)
  (/
    (+
      (/ x (square guess))
      (* 2 guess)
    )
    3)
  )

(define (crt-iter guess x)
  (if (good-enough-cubert? guess x)
    guess
    (crt-iter (improve-cubert guess x)
      x)))

(define (good-enough-cubert? guess x)
  (< (abs (- 1 (/ guess (improve-cubert guess x)))) 0.000000001))
