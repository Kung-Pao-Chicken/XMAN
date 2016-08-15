# 284 rabin_rsa

根据老师上课讲的中国剩余定理，写了个脚本
	
	from Crypto.PublicKey import RSA
	import rsa
	from libnum import *

	pub = RSA.importKey(open('/Users/LSR/Downloads/506d3331-94f1-426c-90f6-b853535d8088 (1)/public.pem').read())
	n = long(pub.n)
	e = long(pub.e)
	print 'n=',n
	print 'e=',e
	def egcd(a, b):
    if a == 0:
        return (b, 0, 1)
    else:
        g, y, x = egcd(b % a, a)
        return (g, x - (b // a) * y, y)

	def modinv(a, m):
    	g, x, y = egcd(a, m)
    	if g != 1:
        raise Exception('modular inverse does not exist')
    	else:
        	return x % m

	p = 275127860351348928173285174381581152299
	q = 319576316814478949870590164193048041239
	c = 12870461690472653980410403828864964322684858768038625885034938328620415737145
	print c



	def	 decrypt_rabin(p, q, c):
    	n = p * q
    	m1 = pow(c, (p + 1) / 4, p)
    	m2 = pow(c, (q + 1) / 4, q)
    	u = modinv(q, p)
    	v = modinv(p, q)
    	m_1 = ((m1 * u * q) + (m2 * v * p)) % n
    	m_2 = ((m1 * u * q * -1) + (m2 * v * p)) % n
    	m_3 = ((m1 * u * q) + (m2 * v * p * -1)) % n
    	m_4 = ((m1 * u * q * -1) + (m2 * v * p * -1)) % n
    	return n2s(m_1),n2s(m_2), n2s(m_3), n2s(m_4)
		print "Rabino sifras:"
	m1, m2, m3, m4 = decrypt_rabin(p, q, c)
	print m1,'\n'
	print m2,'\n'
	print m3,'\n'
	print m4,'\n'
	
于是M1为flag

	D?#???P?bflag{Rab1n_i5_c00l}