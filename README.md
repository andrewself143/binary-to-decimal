# binary-to-decimal
<br>
A calculator I made in Python to convert binary numbers to decimal (i.e. 1001 -> 9).<br>

The script starts by first getting input from the user.<br>

	def get_base():
			base= input('Enter starting base: ')
			return int(base)

	def get_new():
			new=input('Enter desired base: ')
			return int(new)

Then I convert the number into decimal from its starting base.<br>

		def convert_to_decimal(num,base):
				nums=[int(element) for element in num]
				nums.reverse()
				decimal=0
				for exp,i in enumerate(nums, 0):
						#print(i,base, exp)
						decimal+= i*(base**exp)
				return decimal

Finally I call this function which recursively determines the greatest unknown digit in the sequence of numbers.<br>

	def new_base(num,base,exp):       
			highest_num = 0
			highest_val= 0
			cur_exp = -1
			highest_exp = 0
			while True:
					#print("DEBUG")
					cur_exp +=1
					for i in range(0,base):
							val = i*(base**cur_exp)
							if (val < num) and (val > (highest_val)):
									highest_num = i
									highest_val = val
									highest_exp = cur_exp
							if val == num:
									zeroes = buildStr(exp-cur_exp-1)
									moreZeroes = buildStr(cur_exp)
									return zeroes+str(i)+moreZeroes
							if val > num:
									new = num - highest_val
									zeroes = buildStr(exp - cur_exp-1)
									return  zeroes + str(highest_num) + new_base(new, base, highest_exp)
