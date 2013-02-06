# Rubytest.vim

Rubytest.vim is a vim (http://www.vim.org) plugin, which helps you to run ruby test (including vanilla test, rspec, shoulda etc.) in vim.

### Installation

Copy all files to your `~/.vim` directory or use [Vundle](https://github.com/gmarik/vundle) or [Pathogen](https://github.com/tpope/vim-pathogen).

### Usage

After installation, press `<Leader>t` will run the test under your cursor if you are editing a ruby test file.

example:

    $ cd <your rails/merb root>
    $ vim test/unit/user_test.rb

    move cursor into a test case, press <Leader>t

(`<Leader>` is mapping to `\` by default in vim)

---

By default, only test errors will be shown to you. If some of your tests failed, the errors will be displayed in vim's quickfix window, and you can quick jump to the place where the error raise in source file by moving cursor onto the error message and press return (or ctrl-w return to open a new window and jump). If you don't want quickfix, just want to run tests and get results you can set `g:rubytest_in_quickfix` to `0` in your `.vimrc` file:

    let g:rubytest_in_quickfix = 0

---

You can customize the command which will be used to run the test case by settting these options in your vimrc file:

    let g:rubytest_cmd_test          = "ruby %p"
    let g:rubytest_cmd_testcase      = "ruby %p -n '/%c/'"
    let g:rubytest_cmd_spec          = "spec -f specdoc %p"
    let g:rubytest_cmd_spec_example  = "spec -f specdoc %p -e '%c'"
    let g:rubytest_cmd_rspec         = "rspec %p"
    let g:rubytest_cmd_rspec_example = "rspec %p -e '%c'"
    let g:rubytest_cmd_feature       = "cucumber %p"
    let g:rubytest_cmd_story         = "cucumber %p -n '%c'"

(`%p` will be replaced by the path of test file, `%c` will be replaced by the name of test case under cursor)

**For those using Turnip instead of Cucumber, you can run those out of the box by setting the customized commands for feature and story**

    let g:rubytest_cmd_feature  = "rspec %"
    let g:rubytest_cmd_story    = "rspec % --example '%c'"

Note for `rubytest_cmd_story`, this has to be name of the Scenario. Using a line number will run the test, but it filters out everything and nothing gets tested.


### Default Key Bindings

`<Leader>t` run test case under cursor  
`<Leader>T` run all tests in file  
`<Leader>l` run the last test, from any buffer

You can change default key bindings:

    map <Leader>\ <Plug>RubyTestRun     " change from <Leader>t to <Leader>\
    map <Leader>] <Plug>RubyFileRun     " change from <Leader>T to <Leader>]
    map <Leader>/ <Plug>RubyTestRunLast " change from <Leader>l to <Leader>/

---

### Contributors

* Bogdan Gusiev
* Yung Hwa Kwon (nowk)
* J. Weir
* Ben Simpson (bsimpson)
