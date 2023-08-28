# Particles Pico-8

```lua

function make_smoke(x, y, init_size, col)
	local s = {}
	s.x = x
	s.y = y
	s.col = col
	s.width = init_size
	s.width_final = init_size + rnd(3) + 1
	s.t = 0
	s.max_t = 30 + rnd(10)
	s.dx = (rnd(.8)*.4)
	s.dy = rnd(.05)
	s.ddy = .02
	add(smoke, s)
end

function _init()
	smoke = {}
	cursorx = 25
	cursory = 25
	color = 7
end

function move_smoke(sp)
	if (sp.t > sp.max_t) then
		del(smoke, sp)
	end
	if (sp.t > sp.max_t + 15) then
		sp.width += 1
		sp.width = min(sp.width, sp.width_final)
	end
	sp.x = sp.x + sp.dx
	sp.y = sp.y + sp.dy
	sp.dy = sp.dy + sp.ddy
	sp.t = sp.t 
end

function _update()
	foreach(smoke, move_smoke)
		if btn(0, 0) then cursorx -= 1 end
		if btn(1, 0) then cursorx += 1 end
		if btn(2, 0) then cursory -= 1 end
		if btn(3, 0) then cursory += 1 end
		if btn(4, 0) then color = flr(rand(16)) end	
		make_smoke(cursorx, cursory, rnd(4), color)
end		

function draw_smoke(s)
	circfill(s.x, s.y, s.width - 1, s.col)
end

function _draw()
	cls()
	foreach(smoke, draw_smoke)
end

```
