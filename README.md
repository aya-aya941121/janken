puts "------------------------------"
puts "あっち向いてホイゲームを始めます。"

def janken
  puts "じゃんけん・・・"
  puts "0(グー) 1(チョキ) 2(パー)"
  select_number = gets.to_i

  unless [0, 1, 2].include?(select_number)
    puts "不正な値です。もう一度入力してください。"
    return janken
  end

  random_number = rand(3)
  case_pattern = 0

  jankens = ["グー", "チョキ", "パー"]
  puts "あなた：#{jankens[select_number]} 相手：#{jankens[random_number]}"
  puts "------------------------------"

  number = select_number - random_number
  case number
  when 0
    puts "あいこです。もう一度じゃんけんをします。"
    return janken
  when 1, -2
    puts "じゃんけんに負けました。あっちむいて・・・"
    case_pattern = 2
  when -1, 2
    puts "じゃんけんに勝ちました。あっちむいて・・・"
    case_pattern = 1
  end

  case_pattern
end

def atchimuitehoi(case_pattern)
  puts "0(上) 1(下) 2(左) 3(右)"
  select_number2 = gets.to_i

  unless [0, 1, 2, 3].include?(select_number2)
    puts "不正な値です。もう一度入力してください。"
    return atchimuitehoi(case_pattern)
  end

  random_number2 = rand(4)
  directions = ["上", "下", "左", "右"]
  puts "あなた：#{directions[select_number2]} 相手：#{directions[random_number2]}"
  puts "------------------------------"

  if select_number2 == random_number2 && case_pattern == 1
    puts "あなたの勝ちです！おめでとう"
    exit
  elsif select_number2 == random_number2 && case_pattern == 2
    puts "あなたの負けです・・・残念"
    exit
  else
    puts "じゃんけんからやり直します。"
    puts "------------------------------"
    case_pattern = janken
    atchimuitehoi(case_pattern)
  end
end

case_pattern = janken
atchimuitehoi(case_pattern)
