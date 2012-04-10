Installation
============

gem install numbers_in_words

or 

sudo gem install numbers_in_words




The file numbers_to_words defines a module NumbersToWords which is included in Fixnum and Bignum.
The in_words method can then be used on any Fixnum or Bignum object.

E.g.
	>require 'numbers_in_words'
	>112.in_words
	 => one hundred and twelve
	>"one googol".in_numbers
	 =>10000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000 
        >"Seventy million, five-hundred and fifty six thousand point eight nine three".in_numbers
         => 70556000.893

---------------
Example program

To try it out the program display_numbers_to_words.rb expects two integer parameters to define a
range. It then prints out all numbers in words included in this range.

e.g.

	>ruby display_numbers_to_words.rb 1 11
	one
	two
	three
	four
	five
	six
	seven 
	eight
	nine
	ten
	eleven

Whilst creating this project I realized that in English:

* Numbers are grouped in groups of threes
* Numbers less than 1,000 are grouped by hundreds and then by tens
* There are specific rules for when we put an "and" in between numbers

It makes sense to manage the numbers by these groups, so 
I created a method groups_of which will split any integer into
groups of a certain size. It returns a hash with the power of ten
as the key and the multiplier as the value. E.g:

	> 31245.groups_of(3) 
	#=>
	 {0=>245,3=>31} #i.e. 31 thousands, and 245 ones

	> 245.group_of(2)
	#=>
	{0=>45,2=>2}    #i.e. 2 hundreds, and 45 ones

I also created a method group_words takes a block and a size parameter 
This method which could be used by different languages.
(In Japanese numbers are grouped in groups of 4, so it makes sense to try and
separate the language related stuff from the number grouping related stuff)

Example of usage:
	245.group_words(2,"English") do |power, name, digits|
	   puts "#{digits}*10^#{power} #{digits} #{name}s"
	end

	2*10^2= 2 hundreds
	45*10^0 = 45 ones

Future plans
============

* Handle complex numbers
* Option for outputting punctuation
* Reject invalid numbers
* Support for other languages