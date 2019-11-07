import java.awt.BorderLayout;
import java.awt.event.*;
import java.util.*;
import javax.swing.*;

public class life 
{ 
	
	public static void main(String[] args) 
	{ 
		
		//Creating the GUI
		
		JFrame frame = new JFrame("Game of Life");
        frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        frame.setSize(1500, 800);
        
        JTextArea game = new JTextArea(); 
        game.setEditable(false);
        JPanel panel = new JPanel(); 
        JLabel label_M = new JLabel("Rows:");
        JLabel spacer = new JLabel("                           ");
        JLabel label_N = new JLabel("Collumns:");
            
        JSlider slider_M = new JSlider(); 
        slider_M.setMinorTickSpacing(10);
        slider_M.setPaintTicks(true);
        slider_M.setPaintLabels(true);
        slider_M.setMaximum(40);
        slider_M.setMinimum(10);
        Hashtable<Integer, JLabel> position = new Hashtable<Integer, JLabel>();
        position.put(10, new JLabel("10"));
        position.put(20, new JLabel("20"));
        position.put(30, new JLabel("30"));
        position.put(40, new JLabel("40"));
        slider_M.setLabelTable(position);
        
        JSlider slider_N = new JSlider(); 
        slider_N.setMinorTickSpacing(10);
        slider_N.setPaintTicks(true);
        slider_N.setPaintLabels(true);
        slider_N.setMaximum(100);
        slider_N.setMinimum(10);
        Hashtable<Integer, JLabel> position_N = new Hashtable<Integer, JLabel>();
        position_N.put(10, new JLabel("10"));
        position_N.put(50, new JLabel("50"));
        position_N.put(100, new JLabel("100"));
        slider_N.setLabelTable(position_N);

        JButton start = new JButton("Start");
        start.addActionListener(new ActionListener() 
        {
            @Override
            public void actionPerformed(ActionEvent e) 
            {
            	int M = ((JSlider)slider_M).getValue(); 		//retrieving the slider values
          		int N = ((JSlider)slider_N).getValue();
          		try 
          		{
					createGrid(M,N, game);						//Call the createGrid method
				} 
          		catch (InterruptedException e1) 
          		{
					e1.printStackTrace();
				}
            }
        });
        panel.add(label_M); 
        panel.add(slider_M);
        panel.add(spacer);
        panel.add(label_N); 
        panel.add(slider_N);
        panel.add(start);
        frame.add(game);
        frame.getContentPane().add(BorderLayout.SOUTH, panel);	//put the controls at the bottom of the GUI
        frame.setVisible(true);	
	} 
	
	static void createGrid(int M, int N, JTextArea game) throws InterruptedException
	{
		int [][] grid = new int [M][N];
		for (int i = 0; i < grid.length; i++) 
		{
		    for (int j = 0; j < grid[i].length; j++) 
		    {
		        grid[i][j] = (int)(Math.random()*2);			//creates the grid randomly
		    }
		}
 
		for (int i = 0; i < M; i++) 
		{ 
			String line = "";					//set the line to be blank
			for (int j = 0; j < N; j++) 
			{ 
				if (grid[i][j] == 0) 
				{
					line = line+"  ";			//add a blank space to the line
				}
				else
				{
					line = line+" # ";			//add a  # to the line, this represents the living cell
				}
			}
			game.append(line);
			game.append("\n");					//new line for the next line of the 2D array
		}
		game.update(game.getGraphics());
		Thread.sleep(2000);
		game.setText(null);
		
		int [][] next_grid = new int [M][N];
		for (int p = 0; p<200; p++)				//200 iterations
		{
			if(p == 0)
			{
				next_grid = nextIteration(grid, M, N, game);	//the first iteration uses the randomly generated grid
			}
			else
			{
				next_grid = nextIteration(next_grid, M, N, game);	//the rest of the iterations use the next grid created in the nextIteration method
			}
		}
	}

	static int[][] nextIteration(int grid[][], int M, int N, JTextArea game) throws InterruptedException 
	{ 
		int[][] nextGeneration = new int[M][N]; 				//declare a new 2D int array to store the updated values

		for (int x = 1; x < (M - 1); x++) 
		{ 
			for (int y = 1; y < (N - 1); y++) 
			{ 
				int neighbours = 0; 							//Starting off by setting the alive neighbours to 0 for the selected cell
				for (int i = -1; i <= 1; i++) 
				{
					for (int j = -1; j <= 1; j++) 
					{
						neighbours += grid[x + i][y + j];	 	//go round and add up the neighbours of the cell
					}
				}
		
				neighbours -= grid[x][y]; 						// we counted the cell we are looking at and now need to subtract it from the total value


				// Underpopulation 
				if ((neighbours < 2) && (grid[x][y] == 1))
				{
					nextGeneration[x][y] = 0; 
				}

				// Creation of Life
				else if ((neighbours == 3) && (grid[x][y] == 0)) 
				{
					nextGeneration[x][y] = 1; 
				}
								
				// Overcrowding
				else if ((neighbours > 3) && (grid[x][y] == 1)) 
				{
					nextGeneration[x][y] = 0; 
				}
					
				// Survival
				else
				{
					nextGeneration[x][y] = grid[x][y]; 
				}					
			} 
		} 

		//double for loop to output the updated game of life
		
		for (int i = 0; i < M; i++) 
		{ 
			String line = "";
			for (int j = 0; j < N; j++) 
			{ 
				if (nextGeneration[i][j] == 0)
				{
					line = line+"  ";
				}
				else
				{
					line = line+" # ";
				}
			} 
			game.append(line);
			game.append("\n");
		} 
		game.update(game.getGraphics());
		Thread.sleep(100);
		game.setText(null);			//resetting the JTextArea for the next iteration
		return nextGeneration;
	} 
} 
