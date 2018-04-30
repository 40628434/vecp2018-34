# vecp2018-34  
-- 導入 "js" 模組
    local js = require "js"
    -- global 就是 javascript 的 window
    local global = js.global
    local document = global.document
    -- html 檔案中 canvas　id 設為 "canvas"
    -- 準備繪圖畫布
    local canvas = document:getElementById("canvas")
    -- 將 ctx 設為 canvas 2d 繪圖畫布變數
    local ctx = canvas:getContext("2d")
    
    -- 以下採用 canvas 原始座標繪圖
    flag_w = 600
    flag_h = 400
    circle_x = flag_w/4
    circle_y = flag_h/4
    
    -- 先畫滿地紅
    ctx.fillStyle='rgb(255, 0, 0)'
    ctx:fillRect(0, 0, flag_w, flag_h)
    
    -- 再畫青天
    ctx.fillStyle='rgb(0, 0, 150)'
    ctx:fillRect(0, 0, flag_w/2, flag_h/2)
    
    --白色條紋
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 30, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 85, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 145, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 200, flag_w, flag_h/13) 
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(0, 200, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 200, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 260, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(0, 260, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(300, 325, flag_w, flag_h/13)
    
    ctx.fillStyle='rgb(1000, 1000, 1000)'
    ctx:fillRect(0, 325, flag_w, flag_h/13)
    
    --畫星星
    
    -- 導入 "js" 模組
    local js = require "js"
    -- global 就是 javascript 的 window
    local global = js.global
    local document = global.document
    -- html 檔案中 canvas　id 設為 "canvas"
    -- 準備繪圖畫布
    local canvas = document:getElementById("canvas")
    -- 將 ctx 設為 canvas 2d 繪圖畫布變數
    ctx = canvas:getContext("2d")
    
    
    -- 準備在 canvas 中繪圖
    function draw_line(x1, y1, x2, y2, color)
        color = color or "red"
        ctx:beginPath()
        ctx:moveTo(x1, y1)
        ctx:lineTo(x2, y2)
        ctx.strokeStyle = color
        ctx:stroke()
    end
    
    -- x, y 為中心,  r 為半徑, angle 旋轉角,  solid 空心或實心,  color 顏色
    function star(x, y, r, angle, solid, color)
        angle = angle or 0
        solid = solid or false
        color = color or "#fff"
        -- 以 x, y 為圓心, 計算五個外點
        local deg = math.pi/180
        -- 圓心到水平線距離
        local a = r*math.cos(72*deg)
        -- a 頂點向右到內點距離
        local b = (r*math.cos(72*deg)/math.cos(36*deg))*math.sin(36*deg)
        -- 利用畢氏定理求內點半徑
        rin = math.sqrt(a*a + b*b)
        -- 查驗 a, b 與 rin
        --print(a, b, rin)
        if (solid) then
            ctx:beginPath()
        end
        for i = 0, 4 do
            xout = (x + r*math.sin((360/5)*deg*i+180*deg))
            yout = (y + r*math.cos((360/5)*deg*i+180*deg))
            -- 外點增量 + 1
            xout2 = x + r*math.sin((360/5)*deg*(i+1)+180*deg)
            yout2 = y + r*math.cos((360/5)*deg*(i+1)+180*deg)
            xin = x + rin*math.sin((360/5)*deg*i+36*deg+180*deg)
            yin = y + rin*math.cos((360/5)*deg*i+36*deg+180*deg)
            -- 查驗外點與內點座標
            --print(xout, yout, xin, yin)
            if (solid) then
                -- 填色
                if (i==0) then
                    ctx:moveTo(xout, yout)
                    ctx:lineTo(xin, yin)
                    ctx:lineTo(xout2, yout2)
                else
                    ctx:lineTo(xin, yin)
                    ctx:lineTo(xout2, yout2)
                end
            else
                -- 空心
                draw_line(xout, yout, xin, yin, color)
                -- 畫空心五芒星, 無關畫線次序, 若實心則與畫線次序有關
                draw_line(xout2, yout2, xin, yin, color)
            end
        end
        
        if (solid) then
            ctx.fillStyle = "#fff"
            ctx:fill()
        end
    end
    
    --畫星星
    for i = 0, 5 do
        for j = 0,0 do
            star(25+50*i, 15+65*j, 10, 0, true, "#fff")
        end
    end
    
    for i = 0, 4 do
        for j = 0,0 do
            star(50+50*i, 33+65*j, 10, 0, true, "#fff")
        end    
    end
    
    for i = 0, 5 do
        for j = 0,0 do
            star(25+50*i, 50+65*j, 10, 0, true, "#fff")
        end
    end
    
    for i = 0, 4 do
        for j = 0,0 do
            star(50+50*i, 75+65*j, 10, 0, true, "#fff")
        end    
    end
    
    for i = 0, 5 do
        for j = 0,0 do
            star(25+50*i, 95+65*j, 10, 0, true, "#fff")
        end
    end
    
    for i = 0, 4 do
        for j = 0,0 do
            star(50+50*i, 120+65*j, 10, 0, true, "#fff")
        end    
    end
    
    for i = 0, 5 do
        for j = 0,0 do
            star(25+50*i, 140+65*j, 10, 0, true, "#fff")
        end
    end
    
    for i = 0, 4 do
        for j = 0,0 do
            star(50+50*i, 160+65*j, 10, 0, true, "#fff")
        end    
    end
    
    
    for i = 0, 5 do
        for j = 0,0 do
            star(25+50*i, 180+65*j, 10, 0, true, "#fff")
        end
    end
    
   
  -- 
   -- 導入 "js" 模組
    local js = require "js"
    -- global 就是 javascript 的 window
    local global = js.global
    local document = global.document
    -- html 檔案中 canvas　id 設為 "canvas"
    local canvas = document:getElementById("canvas")
    -- 將 ctx 設為 canvas 2d 繪圖畫布變數
    local ctx = canvas:getContext("2d")
    
    -- 屬性呼叫使用 . 而方法呼叫使用 :
    -- 設定填圖顏色
    ctx.fillStyle = "rgb(0,0,150)"
    -- 設定畫筆顏色
    ctx.strokeStyle = "rgb(0,0,150)"
    
    
    
    -- 乘上 deg 可轉為徑度單位
    deg = math.pi / 180
    
    -- 建立多邊形定點位置畫線函式
    function star(radius, xc, yc, n)
        --radius = 100
        --xc = 200
        --yc = 200
        xi = xc + radius*math.cos((360/n)*deg+0*deg)
        yi = yc - radius*math.sin((360/n)*deg+0*deg)
        ctx:beginPath()
        ctx:moveTo(xi,yi)
        for i = 2, n+1 do
            x = xc + radius*math.cos((360/n)*deg*i+0*deg)
            y = yc - radius*math.sin((360/n)*deg*i+0*deg)
            ctx:lineTo(x,y)
        end
    end
    --藍色大六邊形
    star(200, 200, 200,6)
    ctx:closePath()
    ctx:stroke()
    ctx:fill()
    
    --白色內六邊形
    star(120, 200, 200,6)
    ctx:closePath()
    ctx:stroke()
    ctx.fillStyle = '#fff'
    ctx:fill()
    --藍色圓形
    star(50, 200, 200,1000)
    ctx:closePath()
    ctx:stroke()
    ctx.fillStyle = "rgb(0,0,150)"
    ctx:fill()
    --頂端白色
    star(105, 100, 10,6)
    ctx:closePath()
    ctx.fillStyle = '#fff'
    ctx:fill()
    ctx.strokeStyle = '#fff'
    
    star(105, 200, 10,6)
    ctx:closePath()
    ctx.fillStyle = '#fff'
    ctx:fill()
    ctx.strokeStyle = '#fff'
    
    star(105, 300, 10,6)
    ctx:closePath()
    ctx.fillStyle = '#fff'
    ctx:fill()
    ctx.strokeStyle = '#fff'
    
    
    --圓形中間斜線(正方形組成)
    star(20, 200, 200,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    star(20, 190, 190,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    star(20, 180, 180,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    star(20, 210, 210,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    star(20, 220, 220,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    
    star(20, 230, 230,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    
    star(20, 170, 170,4)
    ctx:closePath()
    ctx.fillStyle =  '#fff'
    ctx:fill()
    

    
    
    
    
    
    
    
    

