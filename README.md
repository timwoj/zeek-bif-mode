# zeek-bif-mode
Emacs major-mode for BIF files in Zeek

This is very basic and needs a lot of work to be truly functional. You'll need
`polymode` to use it.

### Configuration in init.el

This provides BIF highlighting, but shunts the internal C++ code over to
c++-mode.

```
(use-package zeek-bif-mode
  :ensure (:repo "/Users/tim/.emacs.d/custom"))
(use-package polymode
  :ensure t
  :mode("\.bif$" . poly-bif-mode)
  :config
  (define-hostmode poly-bif-hostmode :mode 'zeek-bif-mode)
  (define-innermode poly-cpp-bif-innermode
                    :mode 'c++-mode
                    :head-matcher "^.*%\{"
                    :tail-matcher "^.*%\}"
                    :head-mode 'host
                    :tail-mode 'host)
  (define-polymode poly-bif-mode
                   :hostmode 'poly-bif-hostmode
                   :innermodes '(poly-cpp-bif-innermode)))
```