#!/usr/bin/env ruby
# Requires an empty output.txt file.

class Board
  attr_reader :hash_coords, :next_hash

  def initialize(input_text)
    @text_split = input_text.split("\n")
    @hash_coords = {}
    @text_split.each_with_index do |row,row_i|
      row.split("").each_with_index do |el,el_i|
        @hash_coords[@hash_coords.length+1] = [el_i, row_i] if el == '#'
      end
    end
    @current_hash = @hash_coords[1]
    @next_hash = @hash_coords[2]
    # O(n^2) time complexity is less than ideal but it works
    # O(n) space complexity
  end

  def vert_replacer
    return if @current_hash[1] == @next_hash[1]
    @text_split.each_with_index do |row, row_i|
      row.split("").each_with_index do |el, el_i|
        if row_i <= @hash_coords[@hash_coords.key(@current_hash)+1][1] && row_i > @current_hash[1]
          @text_split[row_i][el_i] = '*' if el_i == @current_hash[0] && @text_split[row_i][el_i] != '#'
        end
      end
    end
  end

  def hor_replacer
    return if @current_hash[0] == @next_hash[0]
    @current_hash[0] < @next_hash[0] ? further_left = @current_hash : further_left = @next_hash
    @current_hash[0] > @next_hash[0] ? further_right = @current_hash : further_right = @next_hash
    @text_split.each_with_index do |row, row_i|
      row.split("").each_with_index do |el, el_i|
        @text_split[row_i][el_i] = '*' if row_i == @next_hash[1] && el_i > further_left[0] && el_i < further_right[0]
      end
    end
  end

  def increment
    return if @next_hash == @hash_coords[-1]
    @current_hash = @hash_coords[@hash_coords.key(@current_hash)+1]
    @next_hash = @hash_coords[@hash_coords.key(@next_hash)+1]
  end

  def write_output_text
    @text_split.each do |row|
      File.open("#{ARGV[1]}", 'a') { |f| f.write("#{row}\n") }
    end
    return if @hash_coords.key(@next_hash) == @hash_coords.length
  end

end

board = Board.new(IO.read("#{ARGV[0]}"))

(board.hash_coords.length-1).times do |n|
  board.vert_replacer
  board.hor_replacer
  board.increment
end

board.write_output_text
