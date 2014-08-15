Klasa Extraction:

package baza;

import java.io.IOException;

import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

public class Extraction 
{
	public void getData() throws IOException
	{
		try
		{
			Document doc = Jsoup.connect("http://www.maz.firms.pl/22,0,1,budownictwo-dom-nieruchomosci.html").get();
			Elements links = doc.select("a[href]");

			Document firma;
			int i = beginning;
			
			//iteracja po wszystkich odnosnikach z firmami na stronie
			while(links.get(i).attr("style").isEmpty())
			{
				//System.out.println(links.get(i).text());
				firma = Jsoup.connect("http://www.maz.firms.pl/" + links.get(i).attr("href")).get();
				System.out.println(firma.title());
				i++;
			}
		}
		catch(IOException e)
		{
			e.printStackTrace();
		}
	}
	
	private static int beginning = 195; //196. w kolei odnosnik to zawsze pierwszy z firmami
										//(niestety bardzo brzydkie rozwiazanie)
}


Klasa Main:

package baza;

import java.io.IOException;



public class Main 
{
	public static void main(String[] args) throws IOException 
	{
		Extraction extract = new Extraction();
		extract.getData();
		
		return;
	}
}
