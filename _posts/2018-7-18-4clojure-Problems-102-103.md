---
layout: post
title: 4clojure Problems 102-103
---

<pre><code class="language-klipse">(ns live.test
  (:require [cljs.test :refer-macros [deftest is run-tests]]))

(defn camel [s]
  (let [words (re-seq #"[a-zA-Z]+" s)
        words (cons (first words)
                    (map clojure.string/capitalize
                      (rest words)))]
    (apply str words)))

(deftest test-102
  (is (= (camel "something") "something"))
  (is (= (camel "multi-word-key") "multiWordKey"))
  (is (= (camel "leaveMeAlone") "leaveMeAlone")))

(defn k [i s]
  (set
    (if (= i 0)
      [#{}]
      (mapcat #(for [p (k (- i 1) %2)] (conj p %))
              s (next (iterate next s))))))

(deftest test-103
  (is (= (k 1 #{4 5 6}) #{#{4} #{5} #{6}}))
  (is (= (k 10 #{4 5 6}) #{}))
  (is (= (k 2 #{0 1 2}) #{#{0 1} #{0 2} #{1 2}}))
  (is (= (k 3 #{0 1 2 3 4}) #{#{0 1 2} #{0 1 3} #{0 1 4} #{0 2 3} #{0 2 4}
                         #{0 3 4} #{1 2 3} #{1 2 4} #{1 3 4} #{2 3 4}}))
  (is (= (k 4 #{[1 2 3] :a "abc" "efg"}) #{#{[1 2 3] :a "abc" "efg"}}))
  (is (= (k 2 #{[1 2 3] :a "abc" "efg"}) #{#{[1 2 3] :a} #{[1 2 3] "abc"} #{[1 2 3] "efg"}
                                    #{:a "abc"} #{:a "efg"} #{"abc" "efg"}})))

(run-tests)
</code></pre>
