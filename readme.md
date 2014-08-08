  pythonic.optparse - Lua-based partial reimplementation of Python's
      optparse [2-3] command-line parsing module.

SYNOPSIS

  local OptionParser = require "pythonic.optparse" . OptionParser
  local opt = OptionParser{usage="%prog [options] [gzip-file...]",
                           version="foo 1.23", add_help_option=false}
  opt.add_option{"-h", "--help", action="store_true", dest="help",
                 help="give this help"}
  opt.add_option{
    "-f", "--force", dest="force", action="store_true",
    help="force overwrite of output file"}

  local options, args = opt.parse_args()

  if options.help then opt.print_help(); os.exit(1) end
  if options.force then print 'f' end
  for _, name in ipairs(args) do print(name) end
      
DESCRIPTION

  This library provides a command-line parsing[1] similar to Python optparse [2-3].

  Note: Python also supports getopt [4].

STATUS
  
  This module is fairly basic but could be expanded.
  
API

  See source code and also compare to Python's docs [2,3] for details because
  the following documentation is incomplete.
  
  opt = OptionParser {usage=usage, version=version, add_help_option=add_help_option}
  
    Create command line parser.
  
  opt.add_options{shortflag, longflag, action=action, metavar=metavar, dest=dest, help=help}
  
    Add command line option specification.  This may be called multiple times.
 
  opt.parse_args() --> options, args
  
    Perform argument parsing.
 
DEPENDENCIES

  None (other than Lua 5.1 or 5.2)
  
REFERENCES

  [1] http://lua-users.org/wiki/CommandLineParsing
  [2] http://docs.python.org/lib/optparse-defining-options.html
  [3] http://blog.doughellmann.com/2007/08/pymotw-optparse.html
  [4] http://docs.python.org/lib/module-getopt.html
